# Navisio AI — Benchmark Testing Prompts

> **General strategy**: Each prompt must be tested on Navisio AI first. The same prompt is then submitted to **NotebookLM**, **Gemini Pro**, and **DeepSeek** — both *without* uploading any document (to simulate a generic LLM) and *with* the document uploaded (to simulate a generic RAG system). Record all results in the benchmark Excel spreadsheet.

---

## Comparator Models — Setup Instructions

### Why these four models?

| Model | Type | Why it's useful | How to access |
|-------|------|-----------------|---------------|
| **Navisio AI** | Domain-specific RAG (insurance) | The system under evaluation | [navisio.ai](https://navisio.ai) |
| **NotebookLM** (Google) | Generic RAG | Best "apples-to-apples" RAG comparator — free, cites sources, document-only | [notebooklm.google.com](https://notebooklm.google.com) |
| **Gemini Pro** (Google) | Generic LLM, huge context window | Handles massive PDFs effortlessly without token limits hitting fast | [gemini.google.com](https://gemini.google.com) |
| **DeepSeek** (V3/R1) | Generic LLM with strong reasoning | Excellent free alternative for uploading documents and complex logic | [chat.deepseek.com](https://chat.deepseek.com) |

> **Key insight**: NotebookLM and Navisio both use a RAG approach on uploaded PDFs. The difference is that Navisio is **domain-specialised** (insurance terminology, Italian regulations, IVASS norms). If NotebookLM performs equally well, it means Navisio's specialisation is not adding measurable value — and that becomes your improvement target.

---

### Step-by-Step Benchmark Protocol

Follow this exact procedure for every prompt in Sections 2–5 (document-based tests):

**Step 1 — Navisio AI**
1. Log in to Navisio AI
2. Upload the required document (e.g., DOC-A)
3. Ask the prompt exactly as written
4. Copy the full response into the benchmark spreadsheet
5. Note whether a source citation (page/article) was provided

**Step 2 — NotebookLM**
1. Go to [notebooklm.google.com](https://notebooklm.google.com) and create a new notebook
2. Upload the **same PDF**
3. Ask the **same prompt** in the chat panel
4. Copy the full response + check if sources are cited in the margin panel

**Step 3 — Gemini Pro**
1. Go to [gemini.google.com](https://gemini.google.com) and start a new chat
2. Click the **+ icon** to upload the same PDF (or link from Google Drive)
3. Ask the same prompt
4. Copy the full response

**Step 4 — DeepSeek**
1. Go to [chat.deepseek.com](https://chat.deepseek.com) and start a new conversation
2. Click the **attachment icon** and upload the same PDF
3. Ask the same prompt
4. Copy the full response

**Step 5 — Score and record**
Score each response using the 0–2 rubric (see Benchmark Spreadsheet section) and fill in the Excel row.

> **For Section 1 (knowledge base tests, no documents)**: Skip the file upload step. Just ask the same prompt to all four models in plain chat.
> **Important Rule**: Always open a **NEW CHAT** for each prompt in Section 1. Do not ask all questions in the same chat window, otherwise the model's "memory" will pollute the test results.

---

## Initial Setup: Documents to Use

Gather the following PDFs before starting (all publicly available):

| Label | Suggested Document | Type |
|-------|--------------------|------|
| **DOC-A** | Unipol Condominio Più | Long policy (>100 pages) |
| **DOC-B** | AIG - RC Professionale Avvocati (`AIG_RCP_Avvocati.pdf`) | Medium policy (~50 pages) |
| **DOC-C** | AXA - RC Avvocati (Set Informativo) | Medium policy (~50 pages) |
| **DOC-D** | Any real broker quote (anonymise client data if needed) | Quote/preventivo |
| **DOC-E** | IPID / KID of any simple life or non-life policy | IPID |

> **Note**: If you don't have real PDFs, download them from the IVASS product register or from the official company websites. Use only publicly available documents.

---

## SECTION 1 — "Chiedi a Navisio" (Free-text QA)

*Mode: Open chat, no document upload. Tests Navisio's proprietary insurance knowledge base.*
*For comparators: ask the same prompt in plain chat, no document upload.*
> **Important Rule**: Always open a **NEW CHAT** for each prompt in this section. Do not ask all questions in the same chat window, otherwise the model's "memory" will pollute the test results.

### 1.1 Insurance Knowledge Base (General Questions)

| ID | Prompt | Expected Answer (indicative) | Categories |
|----|--------|------------------------------|------------|
| K-01 | "Qual è la differenza tra una franchigia assoluta e una franchigia relativa?" | Precise technical explanation with numerical examples | Knowledge base, Domain |
| K-02 | "Cosa si intende per coassicurazione e come viene gestita in caso di sinistro?" | Definition + proportional settlement mechanism | Knowledge base |
| K-03 | "Spiegami la normativa IDD: cosa obbliga a fare un broker durante la fase di consulenza?" | Reference to Directive 2016/97/EU, POG obligation, DEMERIT | IVASS/IDD Regulation |
| K-04 | "Cosa cambia tra un'assicurazione 'claims made' e una 'loss occurrence'?" | Technical difference with practical implications for the broker | Knowledge base, Domain |
| K-05 | "Cos'è il principio indennitario e quando non si applica?" | Definition art. 1905 c.c. + exceptions (life, injury) | Knowledge base, Regulation |
| K-06 | "Quali sono i requisiti IVASS per un broker assicurativo in Italia nel 2024?" | Section E/F register, exam, 15 hours mandatory training | IVASS Regulation |
| K-07 | "In una polizza di RC Professionale, cosa si intende per 'retroattività illimitata'?" | Explanation of coverage for facts predating the policy | Knowledge base, Domain |

---

## SECTION 2 — Document QA (File Upload)

*Mode: Upload the PDF, then ask questions. Tests Navisio's RAG pipeline.*
*Follow the Step-by-Step Protocol above for all comparator models.*

### 2.1 Vocabulary Variation — Same concept, different wording

*Objective: verify semantic robustness. Upload **DOC-A** (Unipol Condominio). All three questions below ask the same thing. Open a **NEW CHAT** for each variant.*

| ID | Prompt | Expected Answer | Note |
|----|--------|-----------------|------|
| V-01a | "Qual è la franchigia della polizza per danni da acqua?" | Exact deductible amount from the document | Standard terminology |
| V-01b | "Quanto devo pagare di tasca mia prima che l'assicurazione copra il danno da acqua?" | Same as V-01a | Client-facing terminology |
| V-01c | "Qual è la mia parte del danno non coperta se si rompe un tubo?" | Same as V-01a | Implicit terminology |
| V-02a | "Cosa esclude la polizza?" | Full list of exclusions | Standard terminology |
| V-02b | "Per quali eventi non sono coperto?" | Same as V-02a | Client-facing terminology |
| V-02c | "Dimmi le ipotesi in cui la compagnia non paga" | Same as V-02a | Colloquial terminology |

> **Target metric**: The model should return the same substantive answer for all 3 variants. If the response changes radically based on phrasing, this signals semantic fragility.

### 2.2 Shallow Information (General Extraction)

Upload **DOC-A**.

| ID | Prompt | Expected Answer | Category |
|----|--------|-----------------|----------|
| D-01 | "Quali sono le principali sezioni di copertura (o garanzie) previste da questa polizza?" | List of macro-sections (Danni ai beni, Danni da acqua, RC, Assistenza, Tutela Legale) | Extraction |
| D-02 | "C'è un numero verde per l'Assistenza e in quali orari è attivo?" | 800 070270, active 24/7 (Art. 9.22) | Extraction |
| D-03 | "A chi è stata affidata la gestione dei sinistri per la Tutela Legale?" | ARAG SE, sede di Verona (Art. 9.16) | Extraction |

### 2.3 Information Buried Deep in the Document (Deep Retrieval)

*Objective: Test whether Navisio's RAG can find clauses hidden in the final pages and apply logic.*

Upload **DOC-A**.

| ID | Prompt | Where to find it in the doc | Category |
|----|--------|-----------------------------|----------|
| D-04 | "Ho subito un danno da incendio al contenuto di proprietà condominiale pari a 5.000€. Posso usare il servizio di Riparazione Diretta per non anticipare i soldi?" | NO. Art 9.12 note 21 explicitly says Riparazione Diretta for contents only applies to water and glass, NOT fire. | Deep retrieval, Reasoning |
| D-05 | "Uso il 'Pronto Rientro' per limitare i danni di un sinistro. Se poi si scopre che il sinistro non è indennizzabile, mi addebitate le spese tecniche?" | Unipol reimburses the technical company up to 1.000€ (if in good faith). Max 3.000€/year. (Art. 9.13) | Deep retrieval, Logic |
| D-06 | "Per un sinistro di Tutela Legale vado in disaccordo con la compagnia e si decide per un arbitrato. Chi paga le spese dell'arbitro?" | Split 50/50, unless the outcome is totally favorable to the Assicurato (Art. 9.19) | Deep retrieval, Edge case |
| D-07 | "La Riparazione Diretta vale se il mio condominio si trova in Svizzera?" | NO. Operates only in Italy and Vatican City (Art. 9.12) | Deep retrieval |

> **Specific test for D-04 and D-06**: Verify whether the model cites the exact article (e.g., Art. 9.12 or Art. 9.19) and correctly interprets the exception.

### 2.4 Impossible Questions (Hallucination Test)

Upload **DOC-A**. Since this is a pre-contractual Set Informativo and not a signed policy, it lacks specific client data.

| ID | Prompt | Correct Expected Answer | Category |
|----|--------|-------------------------|----------|
| H-01 | "Chi è il contraente di questa polizza e in che data scade?" | "Not found / This is a pre-contractual document, there is no specific client" | Hallucination |
| H-02 | "Questa polizza copre i danni causati al fabbricato dalla caduta di meteoriti?" | "Not found / not specified in the document" | Hallucination |
| H-03 | "Qual è il massimale esatto in euro previsto dalla polizza per i danni da terrorismo?" | "Not found" or "Massimale is chosen at signing, not present in this blank document" | Hallucination, Reasoning |

> **Red flag**: If any model responds with a specific name, date, or threshold for H-01/H-02/H-03, it is hallucinating. Mark **Hallucinated: Y** in the spreadsheet.

---

## SECTION 3 — Document Comparison (Specific Feature)

*Mode: Use Navisio's "Comparazione documenti" feature. Upload multiple PDFs.*
*For comparators: upload both PDFs simultaneously (Gemini and DeepSeek support this), or paste both texts.*

### 3.1 Quote / Product Set Comparison

Upload **DOC-B** (AIG RC Avvocati) + **DOC-C** (AXA RC Avvocati).

| ID | Prompt | Expected Answer | Category |
|----|--------|-----------------|----------|
| C-01 | "Confronta i massimali di queste due polizze RC Professionale" | Table with single limit, per-claim limit, and aggregate limit for both | Comparison, Structure |
| C-02 | "Quale delle due ha la retroattività più ampia?" | Retroactivity comparison (unlimited vs. X years) with source | Comparison, Deep reasoning |
| C-03 | "Le due polizze coprono entrambe la responsabilità civile verso i dipendenti (RCO) dello studio?" | Yes/No for both + clause reference | Comparison, Reasoning |
| C-04 | "Quali esclusioni sono presenti solo in una delle due polizze ma non nell'altra?" | Differential list of unique exclusions | Advanced comparison |
| C-05 | "Per un giovane studio legale associato con 3 avvocati e 2 praticanti, quale polizza consiglieresti e perché?" | Reasoned recommendation based on the uploaded documents | Commercial reasoning |

### 3.2 Contradictory Information Test

*Objective: Test reasoning on clauses that contradict each other across different articles.*

Use **DOC-A** (Unipol Condominio).

| ID | Scenario | Prompt | Correct Expected Answer | Category |
|----|----------|--------|-------------------------|----------|
| CR-01 | Art. 5 says "water damage is covered". Appendix B says "damage from deliberate pipe rupture is excluded" | "Un vandalo rompe appositamente un tubo causando allagamento: sono coperto?" | "Water damage is covered, BUT deliberate pipe rupture is excluded by a specific clause. The claim may be excluded." | Complex reasoning, Exceptions |
| CR-02 | Art. 12 says "limit €500,000". Art. 25 says "for earthquake damage the limit is reduced to 20%" | "Qual è il massimale in caso di terremoto?" | "€100,000 (20% of €500,000), per specific clause at art. 25" | Complex reasoning, Calculation |

---

## SECTION 4 — Claims Analysis (Specific Feature)

*Mode: Use Navisio's "Check e Analisi Sinistro" feature.*

Upload **DOC-A** and describe a hypothetical claim.

| ID | Prompt | Expected Answer | Category |
|----|--------|-----------------|----------|
| S-01 | "Ho un incendio in un appartamento al 3° piano, causato da un corto circuito dell'impianto elettrico. L'impianto non era a norma. Il danno stimato è €80.000. Come mi comporto?" | 1. Coverage verification, 2. Exclusion check for non-compliant installation (if present), 3. Claim reporting procedure, 4. Required documents, 5. Timelines | Claims analysis, Reasoning |
| S-02 | "Un ladro entra dalla finestra rotta (già rotta prima del furto) e ruba gioielli per €15.000. La polizza ha un limite per i valori preziosi di €5.000. Quant'è l'indennizzo massimo e cosa devo fare?" | Indemnity calculation (€5,000 sub-limit), claim procedure | Claims analysis, Calculation |
| S-03 | "Il sinistro è avvenuto il 10 gennaio 2024 ma me ne sono accorto solo il 15 marzo 2024. La polizza prevede denuncia entro 30 giorni dalla scoperta. Sono ancora in termine?" | Yes, because the 30-day period runs from discovery (March 15), not from the event | Reasoning, Regulation |

---

## SECTION 5 — Traceability (Citations and Sources)

*Objective: Verify whether Navisio correctly cites the source of its answers.*
*After every response that includes specific information (number, clause, exclusion), ask this follow-up:*

| ID | Follow-up Prompt | Expected Answer | Category |
|----|------------------|-----------------|----------|
| T-01 | "Da dove hai preso questa informazione? Mostrami il testo esatto." | Direct quote from the text + page + article | Traceability |
| T-02 | "In quale pagina e articolo del documento hai trovato il massimale di €500.000?" | "Page X, Article Y, which reads: '…'" | Traceability, Citation precision |
| T-03 | "Hai considerato tutte le clausole rilevanti o potresti aver mancato qualcosa?" | Honest answer about potential limitations + suggestion to manually verify | Traceability, Uncertainty |

> **Note on comparators**: NotebookLM shows sources automatically in the side panel — check whether the cited passage actually supports the answer. Gemini and DeepSeek rarely cite exact pages; this is a structural disadvantage vs. Navisio and NotebookLM.

---

## SECTION 6 — Multilingual

| ID | Prompt | Expected Answer | Category |
|----|--------|-----------------|----------|
| ML-01 | Upload an English-language document (e.g., a Lloyd's policy). Ask: "Quali sono le esclusioni principali?" | Italian-language response with the correct content | Multilingual, Translation |
| ML-02 | "What is the deductible for property damage in this policy?" (question in English) | Correct answer (in Italian or English) | Multilingual, Robustness |
| ML-03 | Upload a French-language document (e.g., AXA FR). Ask: "Qual è la franchigia?" | Italian-language response with the correct value | Multilingual |

---

## SECTION 7 — UI Feature Tests

### 7.1 Pre-built Prompts ("Prompt pronti all'uso")

*Go to the pre-built prompts section and test each of the listed categories:*

| Category | What to test | Success signal |
|----------|--------------|----------------|
| **Policy Analysis** | Upload DOC-A, use the pre-built "Analisi completa della polizza" prompt | Structured output covering all main sections (limits, deductibles, exclusions, obligations) |
| **Claims Management** | Use the claims prompt + describe scenario S-01 | Step-by-step operational output |
| **Specific Risks** | Use the RC Professionale prompt on DOC-C | Correct identification of policy type and key coverages |
| **Client Communication** | Ask Navisio to "tradurre in linguaggio semplice per il cliente finale l'esclusione cyber" | Clear text, no jargon, faithful to the original clause |

### 7.2 Export and Output

| ID | Test | Success |
|----|------|---------|
| EX-01 | Generate a comparison report between DOC-B and DOC-C, then export it as PDF | PDF is readable, well-formatted, and cites sources |
| EX-02 | Export the same comparison in Excel/XLSX format | Table is correctly filled with one column per policy |
| EX-03 | Export the report in DOCX format and open it in Word | Document is editable and maintains structure |

---



## Benchmark Spreadsheet — Full Schema

Use this structure in your Excel file (one row per test):

| Test ID | Section | Model | Doc Used | Correctness (0–2) | Completeness (0–2) | Grounding (0–2) | Citation (0–2) | Hallucinated? (Y/N) | Notes (Brief reason for the score) |
|---------|---------|-------|----------|-------------------|--------------------|-----------------|----------------|---------------------|------------------------------------|
| **K-01** | Knowledge | Navisio.AI | none | 2 | 2 | N/A | 2? | N | noted that are general concepts within insurance practice and technique and are not defined by specific legislative or regulatory provisions issued by IVASS |
| K-01 | Knowledge | NotebookLM | none | N/A | N/A | N/A | N/A | N/A |  |
| K-01 | Knowledge | Gemini Pro | none | 2 | 2 | N/A | 1 | N | no citations |
| K-01 | Knowledge | DeepSeek | none | 2 | 2 | N/A | 1 | N | no citations |
| **K-02** | Knowledge | Navisio.AI | none | 2 | 2 | N/A | 2 | N | mentioned the Art.1911, Art. 162 Determinazione dell'oggetto della delega, Art. 1910.(Assicurazione presso diversi assicuratori) and Art. 118 |
| K-02 | Knowledge | NotebookLM | none | N/A | N/A | N/A | N/A | N/A |  |
| K-02 | Knowledge | Gemini Pro | none | 2 | 2 | N/A | 1 | N | only mentioned the Art.1911 about coassicurazione |
| K-02 | Knowledge | DeepSeek | none | 2 | 2 | N/A | 1 | N | only mentioned the Art.1911 about coassicurazione |
| **K-03** | Knowledge | Navisio.AI | none | N/A | N/A | N/A | N/A | N/A |  |
| K-03 | Knowledge | NotebookLM | none | N/A | N/A | N/A | N/A | N/A |  |
| K-03 | Knowledge | Gemini Pro | none | N/A | N/A | N/A | N/A | N/A |  |
| K-03 | Knowledge | DeepSeek | none | N/A | N/A | N/A | N/A | N/A |  |

| D-04 | Doc QA | NotebookLM | DOC-A | 2 | 1 | 2 | 1 | N | Found the rule but citation was vague. |
| D-04 | Doc QA | Gemini | DOC-A | 0 | 0 | 0 | 0 | Y | Invented a 500€ deductible. |
| D-04 | Doc QA | DeepSeek | DOC-A | 2 | 2 | 1 | 0 | N | Perfect answer, but didn't cite the page. |
| C-01 | Compare | Navisio | DOC-B+C | | | | | | |

### Scoring Formula
```
Score = Correctness + Completeness + Grounding + Citation   (max 8 per model)
Score% = Score / 8 × 100
```

### Scoring Rubric

| Dimension | 0 | 1 | 2 |
|-----------|---|---|---|
| **Correctness** | Wrong | Partially correct | Fully correct |
| **Completeness** | Major info missing | Partially complete | Complete |
| **Grounding** | Answer unsupported by document | Partly supported | Entirely supported by document text |
| **Citation** | No citation / wrong citation | Approximate (section only) | Exact (page + article + quote) |

### Results Dashboard

| Feature | Navisio Score% | NotebookLM Score% | Gemini Score% | DeepSeek Score% | Navisio Gap vs best |
|---------|---------------|-------------------|---------------|-----------------|---------------------|
| Knowledge Base | | N/A | | | |
| Document QA (shallow) | | | | | |
| Document QA (deep) | | | | | |
| Comparison | | | | | |
| Claims Analysis | | | | | |
| Hallucination Resistance | | | | | |
| Traceability / Citation | | | | | |
| **TOTAL** | | | | | |

> **N/A** = feature not available for that model.

---

## Recommended Priority Order

Start with these 5 prompts — they best discriminate between mediocre and strong systems:

| Priority | ID | Why it matters |
|----------|----|----------------|
| 🔴 1 | **D-06** | Deep retrieval + nuanced legal reasoning — hardest for generic RAG |
| 🔴 2 | **CR-01** | Contradictory clauses — tests multi-hop reasoning, not just retrieval |
| 🔴 3 | **H-01** | Hallucination guard — essential safety check |
| 🟡 4 | **C-04** | Differential exclusion comparison — Navisio's core use case |
| 🟡 5 | **T-02** | Exact citation — the key differentiator between Navisio and generic models |

> **Next step**: After filling in 30–40 rows, the weakness patterns will emerge clearly. Use them to select the technical pillar (RAG quality, Agentic Pipeline, Constrained Generation, etc.) where your proposed improvement will have the highest measurable impact.
