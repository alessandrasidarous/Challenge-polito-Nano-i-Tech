# Benchmark Results — Navisio AI Challenge @ PoliTo

## Scoring Guide

| Metric | 0 | 1 | 2 |
|--------|---|---|---|
| **Correctness** | Wrong or misleading | Partially correct | Fully correct |
| **Completeness** | Key elements missing | Minor gaps | Fully exhaustive |
| **Grounding** | Not grounded / fabricated | Partially grounded | Fully grounded in source |
| **Citation** | No sources | Section/article (no page) | Exact page or UI citation |

**Hallucinated?**: Y = model returned a factually wrong or fabricated assertion. N = no hallucination.
**Max score per test**: 8 pts. NotebookLM excluded from Knowledge Base (requires doc upload).

---

## SECTION 1 — Knowledge Base (K-tests)

*No documents uploaded. Tests insurance domain knowledge and regulatory accuracy.*

| Test ID | Model | Correctness | Completeness | Citation | Hallu.? | Notes |
|---------|-------|:-----------:|:------------:|:--------:|:-------:|-------|
| **K-01** – Quota-parte formula | Navisio AI | 2 | 2 | N/A | N | Excellent technical explanation, clear examples, and summary table. |
| | DeepSeek | 2 | 2 | N/A | N | Very structured response with formulas, examples, and comparison table. |
| | Gemini Pro | 2 | 2 | N/A | N | Solid explanation with examples, slightly compressed formatting. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-02** – Indennizzo proporzionale | Navisio AI | 2 | 2 | 2 | N | Cited Art. 1911 CC, Art. 162 CAP, and Art. 118 CAP. |
| | DeepSeek | 2 | 2 | 1 | N | Only mentioned Art. 1911 CC. |
| | Gemini Pro | 2 | 2 | 1 | N | Only mentioned Art. 1911 CC. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-03** – IDD Directive | Navisio AI | 2 | 2 | 2 | N | Excellent detail on CAP, IVASS 40/2018, Demands and Needs. Missing explicit POG. |
| | DeepSeek | 2 | 2 | 2 | N | Very comprehensive, explicitly mentions POG and Demands and Needs, cites IDD articles. |
| | Gemini Pro | 2 | 2 | 1 | N | Solid, mentions IBIPs/MiFID II, but only cites the Directive generally. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-04** – Claims made vs Loss occurrence | Navisio AI | 2 | 2 | 2 | N | Perfect technical differentiation, cites Art. 1917 c.c., outlines coverage gap risks. |
| | DeepSeek | 2 | 2 | 0 | N | Excellent practical examples, pros/cons breakdown. |
| | Gemini Pro | 2 | 2 | 0 | N | Clear explanation with examples and summary table. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-05** – Principio indennitario | Navisio AI | 2 | 2 | 2 | N | Excellent, cites Art. 1905 and 1908 CC. |
| | DeepSeek | 2 | 2 | 1 | N | Very clear, covers all exceptions, but missed citing Art. 1905 CC directly. |
| | Gemini Pro | 2 | 2 | 2 | N | Great answer, cites 1905, 1919, 1908 CC, adds practical "valore a nuovo" exception. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-06** – RC Auto obbligatoria limits | Navisio AI | 2 | 2 | 2 | N | Correctly identified Section B, cited laws, gave accurate updated RC limits. |
| | DeepSeek | 1 | 2 | 2 | N | Very detailed and cited laws, but RC limits (1M/1.5M) are outdated. |
| | Gemini Pro | 2 | 2 | 1 | N | Complete answer, lacks specific legislative citations. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |
| **K-07** – Estensione discovery | Navisio AI | 2 | 2 | 2 | N | Perfect explanation. Cites specific internal KB sources (Allianz/Generali). |
| | DeepSeek | 2 | 2 | 0 | N | Clear and distinct explanation, contrasting it with ultrattivita. |
| | Gemini Pro | 2 | 2 | 0 | N | Excellent, highlights "fatto ignoto" requirement and latent damages. |
| | NotebookLM | N/A | N/A | N/A | N/A | N/A — requires document upload |

---

## SECTION 2 — Document QA: Shallow (V-tests)

*Document uploaded (DOC-A: Unipol Condominio Piu). Tests surface-level data retrieval.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **V-01a** | Navisio AI | 2 | 2 | 2 | 2 | N | Accurate extraction with specific page citations. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Excellent structure, details, and exact page citations. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Accurate extraction, mentions sections but no specific pages. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Great categorization, exact UI citations. |
| **V-01b** | Navisio AI | 2 | 2 | 2 | 2 | N | Passed semantic robustness test perfectly, cited pages. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Passed semantic test, added info on 'perdite occulte'. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Passed semantic test, highlighted 'Riparazione Diretta'. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Passed semantic test. Exact UI citations. |
| **V-01c** | Navisio AI | 2 | 2 | 2 | 2 | N | Exceptional: understood phrasing, included sublimits/exclusions. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Passed semantic test. Excellent structure, cited exact page 47. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Passed semantic test. Mentions sections but no exact pages. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Exceptional: included sublimits and exclusions. Exact UI citations. |
| **V-02a** | Navisio AI | 2 | 2 | 2 | 2 | N | Excellent extraction across all sections. Cited exact pages/articles. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Excellent extraction. Mentions section names. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Excellent extraction. Mentions section names. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent extraction. Exact UI citations. |
| **V-02b** | Navisio AI | 2 | 2 | 2 | 2 | N | Passed semantic robustness test perfectly, cited pages. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Passed semantic robustness test perfectly. Cited section numbers. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Passed semantic robustness test perfectly. Mentions section names. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Passed semantic robustness test perfectly. Exact UI citations. |
| **V-02c** | Navisio AI | 2 | 2 | 2 | 2 | N | Excellent extraction across all sections. Cited exact pages. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Exceptional semantic understanding (included forfeiture rules). |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Excellent extraction. Mentions section names. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Exceptional semantic understanding (included forfeiture rules). Exact UI citations. |

---

## SECTION 2b — Document QA: Deep (D-tests)

*Same document. Tests complex clause retrieval, edge cases, and cross-referencing.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **D-01** – Obblighi assicurato | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect shallow extraction. Excellent citations. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Excellent shallow extraction. Cited section numbers. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Excellent extraction but no citations given. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent extraction. Exact UI citations. |
| **D-02** – Rivalsa compagnia | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect shallow extraction. Cited page 90. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Excellent shallow extraction. Cited section name. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Excellent extraction but no citations given. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent extraction. Exact UI citations. |
| **D-03** – Riparazione diretta | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect shallow extraction. Cited page 89. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Excellent shallow extraction. Cited exact pages inline. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Accurate extraction but no citations given. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent extraction. Exact UI citations. |
| **D-04** – Anticipo indennizzo | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Cited exact Art. 9.12 and Note 21. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Cited exact Note 21 inline. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Correct reasoning, but failed to cite exact article. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Exceptional reasoning. Discovered 'Pronto Rientro' alternative. |
| **D-05** – Exception page 88 | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Found the good-faith 1000€ exception. |
| | DeepSeek | 0 | 0 | 1 | 1 | N | FAIL. Stopped reading at page 87, missed exception on page 88. |
| | Gemini Pro | 2 | 1 | 2 | 0 | N | Good retrieval but missed 3000€ yearly cap and exact citations. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Found the good-faith 1000€ exception. |
| **D-06** – Surroga | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect deep retrieval (run 2 with document). Cited pag 90. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Cited exact Art. 9.19 and page 74. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Correct extraction but failed to cite specific article. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Exact UI citations. |
| **D-07** – Riparazione diretta: geografica | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Clarified Switzerland rules. Cited pag 88. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Perfect deep retrieval. Cited Art 9.12. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Perfect deep retrieval. Cited Art 9.12. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect deep retrieval. Exact UI citations. |

---

## SECTION 2c — Hallucination Resistance (H-tests)

*Tests ability to refuse or correctly handle impossible/missing information.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **H-01** – Contraente/scadenza (not in doc) | Navisio AI | 2 | 2 | 2 | 2 | N | Did not hallucinate. Recognized pre-contractual nature. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Did not hallucinate. Recognized pre-contractual nature. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Did not hallucinate. Recognized pre-contractual nature. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Did not hallucinate. Recognized pre-contractual nature. |
| **H-02** – Meteoriti (edge case) | Navisio AI | 2 | 2 | 2 | 2 | N | Found meteorites clause in Art. 2.1 (Not a hallucination!). |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Found meteorites clause in Art. 2.1 (Not a hallucination!). |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Found meteorites clause in Art. 2.1 (Not a hallucination!). |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Found meteorites clause in Art. 2.1 (Not a hallucination!). |
| **H-03** – Terrorismo limit (no fixed euro) | Navisio AI | 2 | 2 | 2 | 2 | N | Did not hallucinate a euro amount. Correctly explained 50% rule. |
| | DeepSeek | 2 | 2 | 2 | 2 | N | Did not hallucinate. Cited exact pages for 50% rule. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Did not hallucinate. Explained 50% rule. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Did not hallucinate. Explained 50% rule. |

---

## SECTION 3 — Document Comparison (C-tests)

*Two documents uploaded (DOC-B: AIG RC Avvocati, DOC-C: AXA RC Avvocati). Tests cross-document analysis.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **C-01** – Massimali & sub-limits | Navisio AI | 2 | 2 | 2 | 2 | N | Excellent multi-doc comparison. Provided table and exact pages. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Excellent comparison. Identified missing schedule limitation. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Excellent comparison and tabular breakdown. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent comparison. Exact UI citations. |
| **C-02** – Retroattivita | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect comparison of base vs exceptions. |
| | DeepSeek | 2 | 1 | 2 | 0 | N | Missed the 12-month limit on Curatore fallimentare. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Perfect comparison of base vs exceptions. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect comparison. Explained structural differences well. |
| **C-03** – RCO & personale | **Navisio AI 🚨 GAP 🚨** | 2 | 1 | 2 | 2 | N | Detailed, but missed the optional vs automatic nuance. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Perfect comparison. Identified optional vs automatic. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Perfect comparison. Identified optional vs automatic. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect comparison. Excellent explanation of third-party exclusion. |
| **C-04** – Esclusioni unilaterali | Navisio AI | 2 | 2 | 2 | 2 | N | Excellent differential list with precise citations. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Phenomenal breakdown and included a summary table. |
| | Gemini Pro | 0 | 0 | 0 | 0 | N | FAIL — Model returned a canned refusal response. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Outstanding differential analysis. |
| **C-05** – Raccomandazione studio legale | Navisio AI | 2 | 2 | 2 | 2 | N | Excellent commercial reasoning: postuma gratuita + franchigia. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Phenomenal structural breakdown addressing each prompt constraint. |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Recovered well. Excellent reasoning on P.IVA autonomy. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Outstanding practical reasoning regarding trainees and individual P.IVA. |

---

## SECTION 3b — Contradictory Information (CR-tests)

*Tests reasoning under conflicting or apparently contradictory clauses.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **CR-01** – Vandalo rompe tubo | Navisio AI | 2 | 2 | 2 | 2 | N | Flawless: correctly separated 3rd-party dolo from insured's dolo exclusion. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Brilliant logical deduction of causality (accidental vs intentional). |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Solid breakdown of the overlapping guarantees. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Excellent analysis including impact on legal protection (Tutela Legale). |
| **CR-02** – Massimale terremoto | Navisio AI | 2 | 2 | 2 | 2 | N | Perfect extraction of tiered limits and accessory sub-limits. |
| | DeepSeek | 2 | 1 | 2 | 2 | N | Missed accessory limits, but provided exact page citations! |
| | Gemini Pro | 2 | 2 | 2 | 0 | N | Excellent extraction of all limits and sub-limits. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Perfect extraction of tiered limits and accessory sub-limits. |

---

## SECTION 4 — Claims Analysis (S-tests)

*Document uploaded (DOC-A). Simulates real claim scenarios requiring operational + legal reasoning.*

| Test ID | Model | Correct. | Complete. | Grounding | Citation | Hallu.? | Notes |
|---------|-------|:--------:|:---------:|:---------:|:--------:|:-------:|-------|
| **S-01** – Incendio impianto non a norma | **Navisio AI 🚨 GAP 🚨** | 2 | 1 | 2 | 2 | N | Deep legal reasoning, but missed 10-day timeline and advance payment clause. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Perfect procedural guide (10 days, 50% advance, evidence preservation). |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Excellent breakdown of claims procedure and limits. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Extremely thorough operational guide with precise limits and accessory costs. |
| **S-02** – Furto gioielli / finestra rotta | **Navisio AI 🚨 GAP 🚨** | 2 | 2 | 1 | 2 | N | Reverted to 3-day Civil Code rule instead of reading 10-day policy rule. |
| | DeepSeek | 2 | 2 | 2 | 1 | N | Perfect evaluation of exclusion clauses and operational timeline. |
| | Gemini Pro | 2 | 2 | 2 | 1 | N | Excellent structural analysis of lack of 'scasso'. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Brilliant application of 20% penalty logic before the policy sub-limit. |
| **S-03** – Termine denuncia: evento vs scoperta | **Navisio AI 🚨 GAP 🚨** | 1 | 2 | 1 | 2 | Y | Fell into the 30-day trap. Accepted user's false premise without verifying doc. |
| | DeepSeek | 2 | 1 | 2 | 2 | N | Correctly identified the 10-day rule. Missed Art. 1915 consequences nuance. |
| | Gemini Pro | 2 | 1 | 2 | 1 | N | Correctly identified the 10-day rule. Missed Art. 1915 consequences nuance. |
| | NotebookLM | 2 | 2 | 2 | 2 | N | Best response: caught the trap AND explained Art. 1915 legal safety net. |

---

## Results Dashboard

*Scoring: total points earned / total points possible x 100 per section.*
*N/A cells excluded from denominator.*

| Section | Navisio AI | NotebookLM | DeepSeek | Gemini Pro |
|---------|:----------:|:----------:|:--------:|:----------:|
| **1. Knowledge Base** (K-01 to K-07) | **92%** | N/A | 84% | 83% |
| **2a. Doc QA Shallow** (V-01a to V-02c) | **100%** | 100% | 92% | 87.5% |
| **2b. Doc QA Deep** (D-01 to D-07) | **100%** | 100% | 82% | 84% |
| **2c. Hallucination Resistance** (H-01 to H-03) | **100%** | 100% | 97% | 91% |
| **3. Document Comparison** (C-01 to C-05) | **97%** | 100% | 88% | 62% |
| **3b. Contradictory Info** (CR-01 to CR-02) | **100%** | 100% | 88% | 88% |
| **4. Claims Analysis** (S-01 to S-03) | 79% | **100%** | 88% | 85% |
| **OVERALL** | **96%** | **100%** | **88%** | **83%** |

> **Note on Gemini Pro**: the C-04 full failure (0/8) heavily penalizes its Comparison score. Excluding that test, its Comparison rises to ~93%.

---

*Last updated: 2026-10-09*
