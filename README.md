# AI FinOps: Why Cloud Financial Governance Fails for Intelligent Systems — and a Framework for What Replaces It

**Author:** Sathiyan Kutty  
**Affiliation:** Chief AI Officer, EMIDS Healthcare IT  
**Contact:** [linkedin.com/in/skutty](https://www.linkedin.com/in/skutty/)  
**Status:** Submitted to the FinOps Foundation — March 2026  
**License:** CC BY 4.0

---

## Abstract

Enterprise AI spending is growing at an unprecedented rate, yet the financial governance frameworks organisations rely on were designed for a fundamentally different cost structure. Cloud FinOps — the dominant discipline for managing cloud infrastructure expenditure — operates on compute-hour billing, resource-level attribution, and predictable linear scaling. AI systems, by contrast, are denominated in tokens, attributed at the request level, and exhibit nonlinear cost dynamics driven by reasoning chains and autonomous agentic loops that can multiply per-session consumption by one to three orders of magnitude.

This paper makes **four original contributions**:

1. A formal definition of *AI FinOps* as a distinct organisational discipline
2. An **eight-dimension AI Cost Taxonomy** covering every measurable cost category in a production AI deployment
3. A **three-level AI FinOps Maturity Model** (Reactive → Managed → Optimised) with specific, assessable capabilities at each level
4. **Five Governance Questions** that constitute a minimum viable baseline assessment for any organisation deploying AI at scale

---

## Repository Contents

```
ai-finops-framework/
├── README.md                         # This file
├── CITATIONS.md                      # Full annotated reference list
├── aifinops.tex                      # LaTeX source (compile with pdflatex + bibtex)
├── aifinops.bib                      # BibTeX bibliography (19 references)
├── aifinops.pdf                      # Compiled paper (10 pages + appendices)
└── appendices/
    ├── capability-checklist.md       # Appendix A: 14-item self-assessment checklist
    └── token-logging-spec.md         # Appendix B: Minimum viable logging schema
```

---

## Key Contributions

### The AI FinOps Definition

> *AI FinOps is the organisational capability comprising the instrumentation, attribution, governance, and optimisation practices required to manage AI system costs at the token level, with accountability structures that connect AI expenditure to measurable business outcomes across model inference, agentic workloads, and training operations.*

### The Eight-Dimension AI Cost Taxonomy

| # | Category | Unit | Primary Optimisation Lever |
|---|----------|------|---------------------------|
| 1 | Input tokens | Tokens/request | Prompt compression, caching, context window management |
| 2 | Output tokens | Tokens/response | Length constraints, structured response formats |
| 3 | Reasoning tokens | Tokens/chain | Thinking budgets, routing away from reasoning tiers |
| 4 | Tool call overhead | Calls/session | Precision retrieval, tool call batching |
| 5 | Retry & failure | Tokens in failed runs | Checkpointing, retry limits, success rate monitoring |
| 6 | GPU compute (training) | GPU-hours/job | Spot instances, job scheduling, checkpoint frequency |
| 7 | GPU compute (inference) | GPU-hours/deployment | Right-sizing, batch inference, model quantisation |
| 8 | Storage & egress | GB stored/transferred | Data locality, weight caching, egress minimisation |

### The AI FinOps Maturity Model

| Level | Name | Key Characteristic |
|-------|------|--------------------|
| 1 | Reactive | Single line-item spend; post-hoc bill review; no token logging |
| 2 | Managed | Cost tagged by application/team; spend alerts; model selection documented |
| 3 | Optimised | Task-level attribution; automated routing; real-time budget enforcement; cost-per-outcome metrics |

### The Five Governance Questions

> If you cannot answer all five, your organisation is at **Level 1 maturity**.

1. What is our total AI spend this month, broken down by application?
2. Which application or agent consumed the most tokens last week?
3. What percentage of our token spend is reasoning tokens vs. standard output?
4. Did any agent or application exceed its token budget in the last 30 days?
5. What is our cost per successful AI-driven outcome, by use case?

---

## Why This Paper

Cloud FinOps has certifications, tooling, personas, and a mature foundation. AI FinOps has none of these — yet. This paper argues that the gap is not a matter of extension but of architectural replacement: AI systems have a cost structure (tokens, request-level attribution, nonlinear agentic dynamics) that Cloud FinOps frameworks were not designed to address.

The **Jevons Paradox** grounds the urgency: token prices are falling 10× per year, yet enterprise AI budgets are rising — because cheaper tokens make previously uneconomical use cases viable, expanding total consumption faster than unit cost declines. Governance is not rendered unnecessary by falling prices; it is made *more* necessary.

---

## Empirical Grounding

- **Published benchmarks:** Gartner (2025 AI infrastructure forecast), Uptime Institute (GPU utilisation thresholds), CoreWeave S-1 filing (neocloud cost advantage data), token price deflation data (2022–2025)
- **Observed enterprise patterns:** Anonymised findings from enterprise healthcare AI deployments — all four patterns (Level 1 prevalence, agentic undercounting, governance dividend, discovery as first-order value) reflect aggregated, de-identified operational experience

---

## Compile Instructions

Requires a standard TeX Live or MiKTeX installation with the following packages: `times`, `natbib`, `booktabs`, `tabularx`, `mdframed`, `titlesec`, `fancyhdr`, `balance`.

```bash
# Clone the repo
git clone https://github.com/virtuousityai/ai-finops-framework
cd ai-finops-framework

# Compile (four passes for full cross-reference resolution)
pdflatex aifinops.tex
bibtex aifinops
pdflatex aifinops.tex
pdflatex aifinops.tex
```

Output: `aifinops.pdf` (10 pages + 2-page appendix, two-column ACM/IEEE-style format)

---

## Relation to Other Work in This Repository

This paper is the third in a series of applied AI systems research from the `virtuousityai` organisation:

| Repo | Focus | Status |
|------|-------|--------|
| [behavioral-fingerprinting-llm-stability](https://github.com/virtuousityai/behavioral-fingerprinting-llm-stability) | Monitoring LLM agent stability across model upgrades | Active |
| [healthcare-ai-operational-drift](https://github.com/virtuousityai/healthcare-ai-operational-drift) | Operational drift detection in production healthcare AI | Active |
| **ai-finops-framework** (this repo) | Financial governance for enterprise AI systems | Submitted — March 2026 |

---

## Citation

If you use the AI FinOps framework, taxonomy, maturity model, or governance questions in your work, please cite:

```bibtex
@techreport{kutty2026aifinops,
  author      = {Kutty, Sathiyan},
  title       = {{AI FinOps}: Why Cloud Financial Governance Fails for Intelligent
                 Systems --- and a Framework for What Replaces It},
  institution = {EMIDS Healthcare IT},
  year        = {2026},
  month       = {March},
  type        = {White Paper},
  note        = {Submitted to the FinOps Foundation.
                 \url{https://github.com/virtuousityai/ai-finops-framework}}
}
```

---

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt this material for any purpose, provided appropriate credit is given.

---

*EMIDS is a healthcare IT services company specialising in managed care technologies. The views expressed in this paper are those of the author and do not constitute official positions of EMIDS or its clients.*
