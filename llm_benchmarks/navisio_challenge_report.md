# Navisio AI — Benchmark Analysis & Challenge Strategy Report

> Benchmark across 4 models: **Navisio AI**, **NotebookLM**, DeepSeek, Gemini Pro.
> 34 test cases: Knowledge Base, Document QA (Shallow + Deep), Hallucination Resistance,
> Document Comparison, Contradictory Reasoning, Claims Analysis.

---

## Overall Results

| Model | Overall Score | Hallucinations |
|-------|:------------:|:--------------:|
| NotebookLM | **100%** | 0 |
| **Navisio AI** | **96%** | 1 |
| DeepSeek | 88% | 0 |
| Gemini Pro | 83% | 0 |

Navisio is **4 points behind NotebookLM** overall. That gap is small in aggregate but concentrated in a single section: **Claims Analysis (79% vs. 100%)**, where all three of Navisio's failures occurred. Every other section is at 97–100%.

---

## Section-by-Section: Navisio vs. NotebookLM

| Section | Navisio AI | NotebookLM | Gap | Where Navisio lost points |
|---------|:----------:|:----------:|:---:|--------------------------|
| Knowledge Base | 92% | N/A | — | K-01: no citation (N/A by design) |
| Doc QA Shallow | 100% | 100% | 0 | None |
| Doc QA Deep | 100% | 100% | 0 | None |
| Hallucination Resistance | 100% | 100% | 0 | None |
| Document Comparison | 97% | 100% | -3% | C-03: missed optional vs. automatic nuance |
| Contradictory Info | 100% | 100% | 0 | None |
| **Claims Analysis** | **79%** | **100%** | **-21%** | S-01: missed procedure; S-02: wrong timeline; S-03: hallucination |

**The 4-point overall gap is almost entirely explained by Claims Analysis.** If claims performance matched NotebookLM, Navisio's overall score would be ~99.5%.

---

## Navisio's Strengths (Summary)

These are solid and well-differentiated from all competitors:

- **Regulatory citation**: Only model to cite IVASS, CAP articles, and Civil Code with live Normattiva.it links. NotebookLM cannot do this (no KB, no regulatory integration).
- **Exact page citations on documents**: Consistent 2.0/2 across all document tests. Gemini Pro: 0.3/2.
- **Proprietary KB accuracy**: Only model with correct RC Auto limits in K-06. DeepSeek gave outdated values.
- **Multi-document comparison**: 97% with full correctness; Gemini Pro failed C-04 entirely (0/8).
- **Contradictory clause reasoning**: 100%, tied only with NotebookLM.

These strengths are the foundation of the challenge pitch. The rest of this report focuses on the gap.

---

## Gap Analysis: Where NotebookLM Outperformed Navisio

### GAP 1 — Claims Analysis: Procedure vs. Legal Framework (Tests S-01, S-02)

**What happened**: In S-01 (apartment fire, non-compliant electrical system), Navisio produced an excellent legal analysis — citing Arts. 1892, 1893, 1898, 1900 of the Civil Code — but failed to extract the concrete operational steps from the uploaded policy document:
- It did **not** mention the 10-day reporting deadline (Art. 9.1 Unipol)
- It did **not** mention the right to request a 50% advance payment on claims over €30,000
- It did **not** mention the 30-day limit for preserving physical evidence

In S-02 (jewellery theft, broken window), Navisio cited Art. 1913 CC (3-day default) instead of reading the contractual 10-day term — relying on a general legal default when the document provided a specific, more favourable rule.

**NotebookLM's approach**: It reversed the priority — checked the document first, extracted the operational checklist, then added Civil Code provisions as supplementary context.

**Root cause**: Navisio's reasoning pipeline appears to weight regulatory knowledge (Civil Code, IVASS) above document-specific extraction in claim scenarios. The model reaches for its KB first and uses the document to confirm, rather than reading the document first and using the KB to supplement.

**Improvement proposal**:

> **Implement a "Claims Mode" with enforced source hierarchy.**
>
> When a query is classified as a claims-handling request (keywords: sinistro, denuncia, danno, indennizzo, rimborso), apply a fixed reasoning order:
> 1. Extract all relevant clauses from the uploaded document (timelines, obligations, advance payment thresholds, evidence requirements)
> 2. Apply the Civil Code only where the document is silent
> 3. Structure output as: **Action Checklist (with deadlines)** first, then Legal Analysis second
>
> Expected outcome: eliminates the two grounding failures in S-01 and S-02, bringing Claims Analysis from 79% to ~95%.

---

### GAP 2 — Premise Verification: Hallucination from False User Input (Test S-03)

**What happened**: The user asked: *"The policy requires notice within 30 days of discovery. Am I still in time?"* The actual Unipol policy requires notice within **10 days**. Navisio accepted the 30-day premise as true and answered accordingly — producing a legally wrong response with high confidence and precise Civil Code citations (Arts. 1913, 1915).

This is Navisio's **only hallucination** in 34 tests, but it is structurally significant: the error was caused not by a lack of information, but by trusting the user over the document.

**NotebookLM's approach**: It immediately flagged the discrepancy: *"Your premise contains a discrepancy with the contractual terms — the policy states 10 days, not 30."* It then answered the correct question AND added the Art. 1915 legal safety net (late filing ≠ automatic loss of coverage if not doloso).

**Root cause**: Navisio does not currently apply a **premise verification** step before answering. When the user frames a factual assertion as a precondition, the model accepts it without checking it against the uploaded document.

**Improvement proposal**:

> **Add a Premise Verification layer to the RAG pipeline.**
>
> Before generating a response, extract any factual assertions from the user's prompt (dates, amounts, timelines, conditions) and run a similarity search against the indexed document. If the assertion contradicts the document with high confidence, inject a correction prefix into the response:
>
> *"Note: the uploaded policy specifies [X], not [Y] as stated in your question. Answering based on the document:"*
>
> This is not a refusal — it is a correction. The answer continues, but grounded in the right information.
>
> Expected outcome: eliminates the S-03 hallucination and turns the failure into a differentiating feature: *"Navisio corrects you when your premise is wrong — other models agree with you."*

---

### GAP 3 — Structural Depth in Multi-Document Comparison (Test C-03)

**What happened**: In C-03 (RCO / Employers' Liability comparison between AIG and AXA), Navisio correctly described what both policies cover but missed the structurally critical distinction: in the AXA policy, RCO is **included automatically** in the base coverage; in the AIG policy, it is an **optional add-on** requiring explicit activation. This distinction has direct premium and coverage implications.

**NotebookLM's approach**: It added an explicit structural dimension — labelling each coverage as "incluso automaticamente" vs "opzionale su richiesta", and noting the consequence: an insured who forgets to activate the option is unprotected.

**Root cause**: Navisio's comparison logic operates on a *content* level ("is X covered?") but not on a *structural* level ("how is X activated?", "at what cost?", "by default or by election?"). This is a gap in the comparison prompt template, not in the underlying model.

**Improvement proposal**:

> **Add structural metadata dimensions to the comparison output schema.**
>
> For each coverage identified in a multi-document comparison, require the model to populate:
> - **Activation**: automatic / optional / conditional
> - **Cost**: included in base premium / additional premium
> - **Scope trigger**: always-on / requires explicit claim / requires prior declaration
>
> This can be enforced via prompt engineering (output schema) or via a structured extraction step before the comparison synthesis.
>
> Expected outcome: closes the C-03 gap, and substantially increases the commercial value of the comparison feature — the broker can see at a glance which coverages require client action.

---

### GAP 4 — Claims Output Format: Legal Brief vs. Operational Checklist

**What happened** (all S-tests): Navisio's claims responses are written as professional legal briefs — deep, accurate, well-cited — but organized around legal categories (which clause applies, what the law says) rather than around what the client needs to do and when.

NotebookLM consistently structured its claims responses as:
1. **Immediate actions** (secure the premises, call the fire brigade, preserve evidence)
2. **Reporting obligations** (who to notify, how, within what deadline)
3. **Financial management** (advance payment rights, adjustment process, timeline to payment)
4. **Legal nuances** (Civil Code fallbacks, what happens if you're late)

Navisio did the opposite: legal nuances first, operational checklist last or never.

**Improvement proposal**:

> **Enforce a standard output template for Claims Analysis mode.**
>
> ```
> ## Claims Summary
> [One-line verdict: covered / not covered / conditional]
>
> ## Immediate Actions
> - [ ] [Action] — deadline: [X days from event/discovery]
> - [ ] [Action]
>
> ## What You Are Entitled To
> - Advance payment: [Y%] if damage > [€Z] (Art. X.X)
> - Repair: [direct / standard / not available]
>
> ## Legal and Contractual Notes
> [Civil Code, exclusions, edge cases]
> ```
>
> This template can be implemented as a system prompt extension for the Claims Analysis feature — no model fine-tuning required, prompt engineering only.

---

### GAP 5 — Completeness on Accessory Costs and Sub-Limits (Test CR-02, S-01)

**What happened**: In several tests, Navisio correctly identified the primary limit or coverage but omitted the accessory sub-limits that are often equally important in practice:
- CR-02: correctly found the 50/70/100% tiered earthquake limit but (in the first pass) did not surface the demolition/removal sub-limit (10% of indemnity, max €20,000) or the design/project management cap (€5,000)
- S-01: did not mention the accessory cost coverage for debris removal (20% of indemnity, max €100,000) or provisional works (20%, max €50,000)

NotebookLM retrieved all accessory limits unprompted in both tests.

**Root cause**: The model's retrieval step likely retrieves the most semantically relevant chunks (main coverage clause) without exhaustively scanning for sub-clauses and accessory limits in adjacent paragraphs.

**Improvement proposal**:

> **Implement a "completeness sweep" for financial limits.**
>
> After the main answer is generated, run a secondary retrieval pass specifically targeting: monetary limits, sub-limits, caps, deductibles, and excess clauses adjacent to the retrieved chunks. If any are found, append them to the answer in a dedicated "Limits & Sub-limits" section.
>
> This mirrors how an experienced adjuster reads a policy: find the main clause, then sweep the surrounding articles for any modifying limits.

---

### GAP 6 — No Art. 1915 Consequence Analysis in Claims (Test S-03)

**What happened**: In S-03 (late claim reporting), both DeepSeek and Gemini Pro identified the correct 10-day rule but stopped there. Navisio hallucinated. Crucially, **only NotebookLM** added the legally essential safety net: under Art. 1915 CC, a late filing does not automatically void coverage — the insurer can only reduce the indemnity proportionally to actual prejudice suffered, and only if the delay was non-doloso.

This is exactly the information a client in this situation needs most: *"Yes, you missed the deadline — but you're not necessarily uninsured."*

**Improvement proposal**:

> **Add a "Consequence Analysis" block to deadline-related queries.**
>
> Whenever a response involves a procedural deadline (reporting, evidence preservation, claim filing), automatically append:
> - What happens if the deadline is missed (proportional reduction vs. full forfeiture)
> - Under what conditions is forfeiture applicable (dolo vs. colpa)
> - Whether the client still has recourse
>
> This is high-value information that reduces client anxiety and demonstrates legal depth — exactly where a vertical tool like Navisio should outperform a generic model.

---

## Priority Ranking of Improvements

| # | Improvement | Effort | Impact | Tests Fixed |
|---|------------|:------:|:------:|-------------|
| 1 | Claims Mode: enforced source hierarchy (contract > law) | Medium | High | S-01, S-02 |
| 2 | Premise Verification layer | Medium | High | S-03 |
| 3 | Consequence Analysis block for deadlines | Low | High | S-03 |
| 4 | Standard Claims output template | Low | Medium | S-01, S-02, S-03 |
| 5 | Structural metadata in comparisons | Low | Medium | C-03 |
| 6 | Completeness sweep for accessory limits | Medium | Medium | CR-02, S-01 |

Items 3 and 4 are **prompt engineering only** — zero model changes required, deployable immediately.
Items 1, 2, 5, 6 require RAG pipeline or retrieval adjustments.

---

## Closing Framing for the Challenge

```
Navisio and NotebookLM tied on 6 out of 7 test sections.
The entire gap is concentrated in Claims Analysis.

The root cause is not a knowledge problem — it is a reasoning
priority problem: Navisio reaches for its regulatory KB first
and reads the document second, when it should be the opposite
for operational queries.

The fix is architectural, not a retrain:
  → Source hierarchy in Claims Mode
  → Premise verification before answering
  → Enforced output template

With those three changes, Navisio closes the gap to NotebookLM
while maintaining its unique advantages:
  → Live regulatory KB (NotebookLM has none)
  → Exact page citations
  → Proprietary product database
```

---

*Benchmark conducted: 2026-10-07 to 2026-10-09*
*Author: Alessandro — Challenge @ PoliTo Nano-i-Tech*
