# Appendix A: AI FinOps Capability Assessment Checklist

**Paper:** AI FinOps: Why Cloud Financial Governance Fails for Intelligent Systems — and a Framework for What Replaces It  
**Author:** Sathiyan Kutty, EMIDS Healthcare IT  
**Version:** 1.0 — March 2026

---

## How to Use This Checklist

This 14-item checklist operationalises the AI FinOps Maturity Model for self-assessment by CAIOs and AI Platform Leads. It is designed to be completed without advanced analytics tooling — if a capability is genuinely in place, you should be able to confirm it in under 60 seconds.

**Scoring:**
- **0–4 in place → Level 1 (Reactive):** Your AI spend is effectively ungoverned. Begin with the 30-Day Visibility Sprint.
- **5–10 in place → Level 2 transition:** Core visibility exists but governance controls are incomplete. Focus on items 5–10.
- **11–14 in place → Level 2 / Level 3:** Strong governance foundation. Focus on cost-per-outcome metrics and automated optimisation.

---

## Checklist

### Group 1 — Cost Visibility (Items 1–4)
*Prerequisite: can you see where your money is going?*

| # | Capability | In Place? |
|---|-----------|-----------|
| 1 | Token logging is implemented on **all** production AI applications | ☐ Yes &nbsp;&nbsp; ☐ No |
| 2 | AI costs are attributed (tagged) by application and team — not as a single aggregate line item | ☐ Yes &nbsp;&nbsp; ☐ No |
| 3 | Model-task fit is documented per application (i.e., you know *why* each application uses its current model tier) | ☐ Yes &nbsp;&nbsp; ☐ No |
| 4 | Reasoning tokens are tracked **separately** from standard output tokens | ☐ Yes &nbsp;&nbsp; ☐ No |

**Score (Group 1): ___ / 4**

---

### Group 2 — Budget Governance (Items 5–8)
*Do controls exist to prevent runaway spend?*

| # | Capability | In Place? |
|---|-----------|-----------|
| 5 | Hard session token budgets are set on **all** production AI agents | ☐ Yes &nbsp;&nbsp; ☐ No |
| 6 | Iteration limits are enforced on all agentic loops | ☐ Yes &nbsp;&nbsp; ☐ No |
| 7 | Prompt caching is enabled on high-volume, stable system prompts | ☐ Yes &nbsp;&nbsp; ☐ No |
| 8 | GPU utilisation is measured by workload (not just aggregate) | ☐ Yes &nbsp;&nbsp; ☐ No |

**Score (Group 2): ___ / 4**

---

### Group 3 — Optimisation (Items 9–11)
*Are you actively reducing cost per unit of value?*

| # | Capability | In Place? |
|---|-----------|-----------|
| 9 | Infrastructure tier (hyperscaler / neocloud / on-premise) is matched to actual utilisation profile | ☐ Yes &nbsp;&nbsp; ☐ No |
| 10 | A quarterly model evaluation cadence is established (reviewing whether model tier selection is still optimal) | ☐ Yes &nbsp;&nbsp; ☐ No |
| 11 | Open-source models have been evaluated for eligible workloads (classification, summarisation, routing) | ☐ Yes &nbsp;&nbsp; ☐ No |

**Score (Group 3): ___ / 3**

---

### Group 4 — Financial Integration (Items 12–14)
*Is AI spend connected to business value and financial planning?*

| # | Capability | In Place? |
|---|-----------|-----------|
| 12 | AI budget is structured with a scenario range (base / expected / ceiling) — not a single annual figure | ☐ Yes &nbsp;&nbsp; ☐ No |
| 13 | An ROI bridge has been completed for every active AI use case (cost vs. measurable value) | ☐ Yes &nbsp;&nbsp; ☐ No |
| 14 | A quarterly AI cost review cadence is established with cross-functional attendance (engineering + finance) | ☐ Yes &nbsp;&nbsp; ☐ No |

**Score (Group 4): ___ / 3**

---

## Total Score Summary

| Group | Score |
|-------|-------|
| Group 1 — Cost Visibility | ___ / 4 |
| Group 2 — Budget Governance | ___ / 4 |
| Group 3 — Optimisation | ___ / 3 |
| Group 4 — Financial Integration | ___ / 3 |
| **Total** | **___ / 14** |

---

## Maturity Level Interpretation

| Total Score | Maturity Level | Recommended Action |
|------------|----------------|--------------------|
| 0–4 | **Level 1 — Reactive** | Begin the 30-Day Visibility Sprint (see Section 5 of the paper). Priority: items 1, 2, 4. |
| 5–7 | **Level 1→2 Transition** | Visibility exists but governance is absent. Priority: items 5, 6, 12. |
| 8–10 | **Level 2 — Managed** | Core governance in place. Focus on optimisation and financial integration. Priority: items 9, 13, 14. |
| 11–12 | **Level 2→3 Transition** | Strong governance. Build automated routing and cost-per-outcome reporting. |
| 13–14 | **Level 3 — Optimised** | AI FinOps capability is mature. Shift focus to proprietary AI investment using governance dividend savings. |

---

## The Five Governance Questions (Quick Reference)

Even before completing the full checklist, an organisation can immediately assess its baseline by answering these five questions. If any are unanswerable, the corresponding group above is incomplete.

1. What is our total AI spend this month, broken down by application? *(Group 1)*
2. Which application or agent consumed the most tokens last week? *(Group 1)*
3. What percentage of our token spend is reasoning tokens vs. standard output? *(Group 1)*
4. Did any agent or application exceed its token budget in the last 30 days? *(Group 2)*
5. What is our cost per successful AI-driven outcome, by use case? *(Group 4)*

---

## How to Cite This Checklist

```bibtex
@techreport{kutty2026aifinops,
  author      = {Kutty, Sathiyan},
  title       = {{AI FinOps}: Why Cloud Financial Governance Fails for Intelligent
                 Systems --- and a Framework for What Replaces It},
  institution = {EMIDS Healthcare IT},
  year        = {2026},
  month       = {March},
  type        = {White Paper},
  note        = {Appendix A: Capability Assessment Checklist.
                 \url{https://github.com/virtuousityai/ai-finops-framework}}
}
```

---

*This checklist is part of the `ai-finops-framework` repository. See `README.md` for full context and `aifinops.pdf` for the complete paper.*
