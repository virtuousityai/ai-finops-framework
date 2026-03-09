# Appendix B: Minimum Viable Token Logging Specification

**Paper:** AI FinOps: Why Cloud Financial Governance Fails for Intelligent Systems — and a Framework for What Replaces It  
**Author:** Sathiyan Kutty, EMIDS Healthcare IT  
**Version:** 1.0 — March 2026

---

## Overview

The ten-field schema below constitutes the **minimum viable log record** for AI FinOps instrumentation. It should be emitted by application middleware on every AI API call and stored in a queryable log store (e.g., BigQuery, Snowflake, Elasticsearch, Datadog).

**Design principles:**
- All fields are **required**. Missing values should be logged as `null` rather than omitted — this preserves schema consistency and allows downstream queries to reliably filter on any field.
- The schema is **model-agnostic** — it works across Anthropic, OpenAI, Google, Mistral, and open-source deployments.
- It requires **no changes to application logic or model configuration** — it is a middleware addition only.
- Fields 1–7 can be populated from the API response object alone. Fields 8–10 require application-level context.

---

## The Ten-Field Schema

| # | Field | Type | Required | Description |
|---|-------|------|----------|-------------|
| 1 | `timestamp` | ISO 8601 datetime (UTC) | Yes | Time of API call **completion** (not initiation) |
| 2 | `application_id` | string | Yes | Unique identifier of the calling application (e.g., `prior-auth-agent`, `clinical-doc-v2`) |
| 3 | `team_id` | string | Yes | Team or cost centre owning the application. Maps to your internal cost allocation structure. |
| 4 | `model_id` | string | Yes | Full model identifier as returned by the API (e.g., `claude-sonnet-4-6`, `gpt-4o`, `llama-3.3-70b`) |
| 5 | `input_token_count` | integer | Yes | Total tokens in the full request context, including system prompt, conversation history, and retrieved documents |
| 6 | `output_token_count` | integer | Yes | Tokens in the model's **visible** response only — excludes reasoning tokens |
| 7 | `reasoning_token_count` | integer | Yes | Thinking / reasoning tokens if extended thinking is enabled; `null` if the model does not support or was not configured for reasoning |
| 8 | `tool_calls_count` | integer | Yes | Number of tool invocations in this session turn; `null` for non-agentic single-turn calls |
| 9 | `session_id` | string | Yes | Shared identifier across **all** API calls in a multi-turn session or agentic workflow. Enables per-session cost aggregation. Use `null` for stateless single-turn calls. |
| 10 | `task_type` | enum | Yes | Controlled vocabulary — see values below |

---

## `task_type` Controlled Vocabulary

Use a controlled vocabulary for `task_type` to enable cost analysis by workload category. Recommended values:

| Value | Description | Typical Token Profile |
|-------|-------------|----------------------|
| `classification` | Categorisation, routing, triage | Low input, very low output |
| `summarisation` | Document or conversation summarisation | High input, medium output |
| `generation` | Content, code, or document generation | Medium input, high output |
| `retrieval` | RAG retrieval-augmented generation | Very high input, medium output |
| `reasoning` | Multi-step reasoning, analysis, inference | Medium input, high reasoning tokens |
| `agentic` | Multi-turn autonomous agent execution | Very high total (accumulates across turns) |
| `extraction` | Structured data extraction from unstructured text | High input, low-medium output |
| `other` | Does not fit above categories | Variable |

---

## Example Log Record (JSON)

```json
{
  "timestamp": "2026-03-09T14:32:07.412Z",
  "application_id": "prior-auth-agent",
  "team_id": "managed-care-ops",
  "model_id": "claude-sonnet-4-6",
  "input_token_count": 8241,
  "output_token_count": 412,
  "reasoning_token_count": 3180,
  "tool_calls_count": 4,
  "session_id": "sess_a7f3c9d2",
  "task_type": "agentic"
}
```

**Cost calculation for this record** (illustrative at Q1 2026 pricing):
- Input: 8,241 tokens × $3.00/M = **$0.025**
- Output: 412 tokens × $15.00/M = **$0.006**
- Reasoning: 3,180 tokens × $15.00/M = **$0.048**
- **Total per call: ~$0.079**

Note that reasoning tokens (3,180) exceed output tokens (412) by nearly 8×, and represent 60% of the total cost for this call — invisible without explicit reasoning token tracking.

---

## Implementation Notes

### Anthropic (Claude)
Reasoning tokens are returned in the API response under `usage.cache_creation_input_tokens` for prompt caching and `usage.thinking_tokens` when extended thinking is enabled. Log both separately.

```python
response = client.messages.create(...)
log_record = {
    "input_token_count":     response.usage.input_tokens,
    "output_token_count":    response.usage.output_tokens,
    "reasoning_token_count": getattr(response.usage, "thinking_tokens", None),
}
```

### OpenAI (GPT-4o, o1, o3)
Reasoning tokens for `o1`/`o3` series are returned under `usage.completion_tokens_details.reasoning_tokens`.

```python
response = client.chat.completions.create(...)
log_record = {
    "input_token_count":     response.usage.prompt_tokens,
    "output_token_count":    response.usage.completion_tokens,
    "reasoning_token_count": response.usage.completion_tokens_details.reasoning_tokens
                             if hasattr(response.usage, "completion_tokens_details") else None,
}
```

### Open-Source / Self-Hosted (vLLM, Ollama, LM Studio)
Most open-source inference servers return token counts in their response objects. For servers that do not, use the `tiktoken` or `transformers` tokenizer to count tokens client-side before and after each call.

---

## Recommended Storage Schema (SQL)

```sql
CREATE TABLE ai_token_log (
    id                    BIGSERIAL PRIMARY KEY,
    timestamp             TIMESTAMPTZ       NOT NULL,
    application_id        VARCHAR(128)      NOT NULL,
    team_id               VARCHAR(128)      NOT NULL,
    model_id              VARCHAR(128)      NOT NULL,
    input_token_count     INTEGER           NOT NULL,
    output_token_count    INTEGER           NOT NULL,
    reasoning_token_count INTEGER,
    tool_calls_count      INTEGER,
    session_id            VARCHAR(256),
    task_type             VARCHAR(64)       NOT NULL,

    -- Derived cost columns (populate via ETL using current pricing table)
    input_cost_usd        NUMERIC(12, 8),
    output_cost_usd       NUMERIC(12, 8),
    reasoning_cost_usd    NUMERIC(12, 8),
    total_cost_usd        NUMERIC(12, 8)
);

-- Recommended indexes for FinOps queries
CREATE INDEX idx_token_log_app_time   ON ai_token_log (application_id, timestamp);
CREATE INDEX idx_token_log_team_time  ON ai_token_log (team_id, timestamp);
CREATE INDEX idx_token_log_session    ON ai_token_log (session_id) WHERE session_id IS NOT NULL;
CREATE INDEX idx_token_log_task_type  ON ai_token_log (task_type, timestamp);
```

---

## Minimum Viable Dashboard Queries

Once the log table is populated, these three queries answer Governance Questions 1 and 2 from the paper immediately:

**Q1 — Total spend by application this month:**
```sql
SELECT
    application_id,
    SUM(total_cost_usd)        AS total_cost,
    SUM(input_token_count)     AS input_tokens,
    SUM(output_token_count)    AS output_tokens,
    SUM(reasoning_token_count) AS reasoning_tokens
FROM ai_token_log
WHERE timestamp >= date_trunc('month', NOW())
GROUP BY application_id
ORDER BY total_cost DESC;
```

**Q2 — Highest token consumer last 7 days:**
```sql
SELECT
    application_id,
    team_id,
    SUM(input_token_count + output_token_count
        + COALESCE(reasoning_token_count, 0)) AS total_tokens,
    SUM(total_cost_usd) AS total_cost
FROM ai_token_log
WHERE timestamp >= NOW() - INTERVAL '7 days'
GROUP BY application_id, team_id
ORDER BY total_tokens DESC
LIMIT 10;
```

**Q3 — Reasoning token share by application:**
```sql
SELECT
    application_id,
    SUM(reasoning_token_count)::FLOAT /
        NULLIF(SUM(output_token_count + COALESCE(reasoning_token_count, 0)), 0) * 100
        AS reasoning_pct_of_output_spend
FROM ai_token_log
WHERE timestamp >= date_trunc('month', NOW())
  AND reasoning_token_count IS NOT NULL
GROUP BY application_id
ORDER BY reasoning_pct_of_output_spend DESC;
```

---

## Extending the Schema

Once the 10-field minimum is stable, consider adding these fields for Level 3 maturity:

| Field | Type | Purpose |
|-------|------|---------|
| `latency_ms` | integer | Response latency — correlates cost with performance |
| `cache_hit` | boolean | Whether the call was served from prompt cache |
| `outcome_id` | string | Links to a business outcome record for cost-per-outcome metrics (Q5) |
| `model_tier` | enum (`tier1`\|`tier2`\|`tier3`\|`tier4`\|`tier5`) | Normalised tier label independent of model name |
| `retry_count` | integer | Number of retries — identifies failure cost |
| `budget_remaining_pct` | float | Remaining session budget at call time — enables proactive alerting |

---

## How to Cite This Specification

```bibtex
@techreport{kutty2026aifinops,
  author      = {Kutty, Sathiyan},
  title       = {{AI FinOps}: Why Cloud Financial Governance Fails for Intelligent
                 Systems --- and a Framework for What Replaces It},
  institution = {EMIDS Healthcare IT},
  year        = {2026},
  month       = {March},
  type        = {White Paper},
  note        = {Appendix B: Minimum Viable Token Logging Specification.
                 \url{https://github.com/virtuousityai/ai-finops-framework}}
}
```

---

*This specification is part of the `ai-finops-framework` repository. See `README.md` for full context and `aifinops.pdf` for the complete paper.*
