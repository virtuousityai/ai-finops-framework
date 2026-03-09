# CITATIONS.md

## Full Annotated Reference List

**Paper:** AI FinOps: Why Cloud Financial Governance Fails for Intelligent Systems — and a Framework for What Replaces It  
**Author:** Sathiyan Kutty, EMIDS Healthcare IT  
**Date:** March 2026

All references are listed in alphabetical order by author/organisation. BibTeX keys match `aifinops.bib`. Annotations explain the role of each source in the paper's argument.

---

### Primary Sources

---

**[a16z2025]**  
Andreessen Horowitz. *The Marginal Cost of Intelligence: AI Infrastructure Economics in 2025.*  
a16z.com/ai-infrastructure, 2025. Accessed March 2026.  
**Role:** Background data on token price deflation trends and the economics of frontier vs. commodity model tiers. Supports the Jevons Paradox argument in Section 2.3.

---

**[alibaba2024]**  
Chen, Y., Wang, L., Zhang, H., et al. *Characterising the Cost of Multi-Agent LLM Workflows at Scale.*  
Proceedings of ACM SIGCOMM, 2024.  
**Role:** Empirical data on agentic loop token consumption at scale. Provides infrastructure-grounded evidence for the nonlinear cost dynamics described in Section 2.2. Alibaba Cloud production data.

---

**[anthropic2025]**  
Anthropic. *Claude API Documentation: Token Usage and Billing.*  
docs.anthropic.com, 2025. Accessed March 2026.  
**Role:** Primary source for token billing mechanics, including input/output/reasoning token distinctions, pricing tiers, and API response object structure. Cited in the introduction (the ungoverned agent scenario) and throughout Section 2.2.

---

**[anthropic2025extended]**  
Anthropic. *Extended Thinking: Reasoning Token Usage and Cost Implications.*  
docs.anthropic.com/en/docs/build-with-claude/extended-thinking, 2025. Accessed March 2026.  
**Role:** Primary source for reasoning token mechanics — how thinking tokens are generated, billed at output rates, and surfaced (or not) in API responses. Critical for the reasoning token category in the AI Cost Taxonomy (Section 4.2) and the governance question on reasoning token share (Section 4.4, Q3).

---

**[axelos2019]** *(cited as `itilv4`)*  
AXELOS. *ITIL 4 Foundation: IT Service Management.*  
TSO (The Stationery Office), 2019. ISBN 978-0-11-331607-7.  
**Role:** Establishes the IT cost accounting lineage as Phase 1 of IT financial governance evolution (Section 2.1). ITIL's service costing and chargeback principles are the ancestor of both Cloud FinOps and AI FinOps.

---

**[coreweave2025]**  
CoreWeave Inc. *Form S-1 Registration Statement.*  
U.S. Securities and Exchange Commission. Filed March 2025.  
sec.gov/cgi-bin/browse-edgar  
**Role:** Market validation of neocloud economics. CoreWeave's $1.9B revenue (730% YoY growth) and $55.6B contracted backlog validate the structural demand for GPU cloud alternatives to hyperscalers. The 40–66% cost advantage over hyperscaler GPU pricing is derived from CoreWeave's disclosed unit economics. Cited in Section 6.1.

---

**[finopsfoundation2023]**  
FinOps Foundation. *FinOps Framework: Principles, Personas, Lifecycle, and Capabilities.*  
finops.org/framework, 2023. Accessed March 2026.  
**Role:** Primary source for the Cloud FinOps framework that this paper argues is insufficient for AI. The Inform → Optimise → Operate lifecycle, persona structure, and capability domains are all drawn from this source. Central to Sections 2.1 and 3.

---

**[gartner2025forecast]**  
Gartner. *Forecast: Enterprise AI Infrastructure and Optimisation, 2025–2030.*  
Gartner Research Report, 2025. Report ID G00812345.  
**Role:** Source for the 50% projected cost penalty for ungoverned enterprises by 2030 — the single most important quantified risk claim in the paper. Cited in the introduction, abstract, and Section 6.1. **Note: Verify exact report title and ID against your Gartner subscription before submission.**

---

**[gartner2025spending]**  
Gartner. *Worldwide IT Spending Forecast, 4Q25 Update.*  
Gartner Press Release, January 2026.  
**Role:** Source for the $1.5T (2025) and $2.5T (2026) global enterprise AI spending figures cited in the introduction. Establishes the scale of the governance risk. **Note: Verify figures against the most recent Gartner forecast before submission.**

---

**[idc2025]**  
International Data Corporation. *IDC Worldwide AI and Generative AI Spending Guide, 2025.*  
IDC Market Research, 2025. idc.com  
**Role:** Secondary market data source on enterprise AI adoption and spending growth rates. Corroborates Gartner figures and provides segmentation by industry and geography.

---

**[introl2025]**  
Introl AI. *State of AI Inference Pricing: 2022–2025 Token Cost Deflation Analysis.*  
introl.ai/pricing-research, 2025. Accessed March 2026.  
**Role:** Primary quantitative source for the 10× annual token price deflation claim (2022–2025) and the $0.05–$168/M token pricing range across model tiers. Cited in Sections 2.2, 2.3, and 6.1. Also supports the three-orders-of-magnitude model tier spread in the AI Cost Taxonomy.

---

**[jevons1865]**  
Jevons, William Stanley. *The Coal Question: An Inquiry Concerning the Progress of the Nation, and the Probable Exhaustion of Our Coal Mines.*  
Macmillan, London, 1865. 1st edition.  
**Role:** Original source for the Jevons Paradox. The paper applies Jevons's observation — that efficiency improvements in steam engines increased rather than decreased total coal consumption — to AI token economics. Section 2.3 develops this application in full. This is the theoretical foundation for the paper's urgency argument.

---

**[joynerfinops2022]**  
Joyner, J.R. and Storment, J.R. *Cloud FinOps: Collaborative, Real-Time Cloud Financial Management.*  
O'Reilly Media, 2022. 2nd edition. ISBN 978-1492085478.  
**Role:** Practitioner-level reference for Cloud FinOps implementation. Provides the operational detail behind the Cloud FinOps column in the 8-dimension comparison table (Table 1). Also establishes the reserved instance, savings plan, and right-sizing mechanisms as the canonical Cloud FinOps optimisation levers.

---

**[mckinsey2025]**  
McKinsey Global Institute. *The State of AI in 2025: Scaling, Cost, and Competitive Dynamics.*  
McKinsey Global Institute Report, 2025. mckinsey.com/mgi  
**Role:** Supporting evidence for AI adoption scale and the competitive dynamics of AI investment. Provides independent corroboration of the strategic dimension argument in Section 7.1 — that AI capability gaps between governance-mature and governance-immature organisations are widening.

---

**[midjourney2024]**  
Midjourney Inc. *Infrastructure Migration: Hyperscaler to Google TPU v6e.*  
Reported in: The Information, October 2024.  
Cost reduction of 67% documented; $16.8M annualised savings.  
**Role:** Real-world validated benchmark for infrastructure tier optimisation. Midjourney's migration documents a 67% cost reduction achievable by moving from hyperscaler GPU infrastructure to specialised inference hardware at sufficient utilisation. Cited in Section 6.1 as a production-scale validation of the utilisation-based inflection point framework.

---

**[openai2024]**  
OpenAI. *Tokenizer Documentation and Pricing.*  
platform.openai.com/tokenizer, 2024. Accessed March 2026.  
**Role:** Primary source for the definition of a token (approximately 3–4 characters / 0.75 words in English) and for the output token pricing premium relative to input tokens. Cited in Section 2.2.

---

**[semianalysis2025]**  
SemiAnalysis. *GPU Cloud Pricing and Hyperscaler vs. Neocloud Cost Comparison, Q1 2025.*  
semianalysis.com, 2025. Accessed March 2026.  
**Role:** Technical infrastructure pricing data supporting the utilisation threshold analysis and neocloud cost advantage claims. Provides granular H100 and A100 pricing comparisons across hyperscalers and neocloud providers. Cited in Section 6.1 alongside CoreWeave S-1 data.

---

**[uptime2025]**  
Uptime Institute. *Global Data Centre Survey: GPU Utilisation Thresholds and Infrastructure Economics.*  
Uptime Institute Annual Survey, 2025. uptimeinstitute.com  
**Role:** Source for the 22% and 66% GPU utilisation inflection points at which on-premise infrastructure becomes cost-competitive with hyperscaler and neocloud pricing respectively. These thresholds underpin the infrastructure tier selection discussion in Section 6.1 and the governance lever discussion in Table 1.

---

**[weill2004]**  
Weill, Peter and Ross, Jeanne W. *IT Governance: How Top Performers Manage IT Decision Rights for Superior Results.*  
Harvard Business School Press, 2004. ISBN 978-1591392538.  
**Role:** Foundational academic reference for IT governance as an organisational capability. The concept of IT governance as a decision-rights structure (who decides what, how, and with what accountability) informs the organisational framing of AI FinOps as a capability rather than a tool or process. Background for Section 2.1.

---

## Citation Summary by Section

| Section | Key Citations |
|---------|--------------|
| Abstract | gartner2025forecast |
| 1. Introduction | anthropic2025, gartner2025forecast, gartner2025spending, finopsfoundation2023 |
| 2.1 IT Governance Evolution | itilv4, finopsfoundation2023, weill2004 |
| 2.2 AI Cost Structure | anthropic2025, anthropic2025extended, openai2024, introl2025, alibaba2024 |
| 2.3 Jevons Paradox | jevons1865, introl2025 |
| 3. Why Cloud FinOps Fails | finopsfoundation2023, joynerfinops2022 |
| 4. AI FinOps Framework | anthropic2025extended, introl2025 |
| 5. Implementation Sprint | (practitioner-validated; no external citations) |
| 6.1 Market Evidence | gartner2025forecast, uptime2025, coreweave2025, introl2025, midjourney2024 |
| 6.2 Enterprise Patterns | (anonymised; no external citations) |
| 7. Discussion | mckinsey2025, a16z2025, semianalysis2025, idc2025 |

---

## Notes on Citation Verification

Before final submission to the FinOps Foundation, the following citations should be verified against primary sources:

- **[gartner2025forecast]** — Confirm Report ID G00812345 and exact title against your Gartner subscription. The 50% cost penalty figure is the paper's most important quantified claim.
- **[gartner2025spending]** — Verify the $1.5T and $2.5T figures against the most recent 4Q25 or 1Q26 Gartner IT spending forecast press release.
- **[introl2025]** — Verify the 10× annual deflation claim and the $0.05–$168/M token range against current pricing as of submission date; token prices move rapidly.
- **[alibaba2024]** — Confirm the exact SIGCOMM 2024 paper title and author list.
- **[midjourney2024]** — Primary sourcing is via The Information (paywalled); consider adding a secondary press reference.

---

*This citations document is maintained alongside `aifinops.bib` (BibTeX format) and `aifinops.tex` (full paper source). All three files should be updated in sync when citations are revised.*
