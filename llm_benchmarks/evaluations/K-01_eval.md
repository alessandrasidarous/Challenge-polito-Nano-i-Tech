# Evaluation: K-01

**Prompt**: "Qual è la differenza tra una franchigia assoluta e una franchigia relativa?"
**Expected Answer**: Precise technical explanation with numerical examples.
**Category**: Knowledge base, Domain
**Doc Used**: None

---

## 1. Navisio AI

**Output**: 
La differenza fondamentale tra franchigia assoluta e franchigia relativa risiede nel modo in cui l'assicuratore calcola l'indennizzo quando il danno supera l'importo della franchigia stabilito in polizza (trattandosi di istituti di tecnica contrattuale standard del mercato assicurativo).

1. Franchigia Assoluta
La franchigia assoluta rimane sempre a carico dell'assicurato, indipendentemente dall'ammontare complessivo del danno. L'assicuratore risarcisce soltanto la quota di danno che eccede la cifra pattuita.
Danno pari o inferiore alla franchigia: l'assicuratore non versa alcun indennizzo.
Danno superiore alla franchigia: l'assicuratore indennizza il danno detraendo l'importo della franchigia.
Esempio: con una franchigia assoluta di 200 €: Danno di 150 € → Indennizzo = 0 € (a carico dell'assicurato). Danno di 1.000 € → Indennizzo = 800 € (1.000 € - 200 €).

2. Franchigia Relativa
La franchigia relativa opera come una soglia di risarcibilità. Se il danno supera l'importo della franchigia, la franchigia decade integralmente e l'assicuratore indennizza il danno per l'intero ammontare.
Danno pari o inferiore alla franchigia: l'assicuratore non versa alcun indennizzo (il danno resta interamente a carico dell'assicurato).
Danno superiore alla franchigia: l'assicuratore paga il 100% del danno, senza applicare alcuna detrazione.
Esempio: con una franchigia relativa di 200 €: Danno di 150 € → Indennizzo = 0 € (il danno non supera la soglia). Danno di 1.000 € → Indennizzo = 1.000 € (superata la soglia, l'indennizzo è integrale).

Sintesi comparativa (Tabella)
...

**Evaluation**:
- **Correctness**: 2 (Fully correct)
- **Completeness**: 2 (Complete)
- **Grounding**: N/A
- **Citation**: N/A
- **Hallucinated?**: N
- **Notes**: Excellent technical explanation. The examples are clear and the summary table is very useful.

---

## 2. DeepSeek

**Output**: 
La differenza principale tra franchigia assoluta e franchigia relativa riguarda il modo in cui viene calcolato l'indennizzo quando si verifica un sinistro.

🔹 Franchigia assoluta
È la forma più comune. La franchigia è sempre a carico dell'assicurato, indipendentemente dall'importo del danno.
Formula: Indennizzo = Danno – Franchigia
Esempio: Franchigia 500 €, danno 2.000 € → l'assicurato riceve 1.500 €.
Esempio 2: Franchigia 500 €, danno 400 € → l'assicurato non riceve nulla (il danno è sotto la franchigia).

🔹 Franchigia relativa
Funziona come una soglia: se il danno supera la franchigia, questa non viene detratta e l'assicurazione copre l'intero importo.
Formula: Se Danno > Franchigia → Indennizzo = Danno (intero)
Esempio: Franchigia 500 €, danno 2.000 € → l'assicurato riceve 2.000 €.
Esempio 2: Franchigia 500 €, danno 400 € → l'assicurato non riceve nulla.

📊 In sintesi (Tabella)
...

**Evaluation**:
- **Correctness**: 2 (Fully correct)
- **Completeness**: 2 (Complete)
- **Grounding**: N/A
- **Citation**: N/A
- **Hallucinated?**: N
- **Notes**: Very structured response with formulas, distinct examples, and a clear comparison table.

---

## 3. Gemini Pro

**Output**: 
La differenza principale riguarda quando e quanto l'assicurazione paga in caso di sinistro.Franchigia Assoluta: È una somma fissa che viene sempre detratta dal risarcimento, indipendentemente dall'entità del danno. L'assicurazione rimborsa solo la parte di danno che supera questa cifra.Esempio: Hai una franchigia assoluta di 500€ e subisci un danno di 1.200€. L'assicurazione ti rimborsa 700€ (1.200 - 500). Se il danno è di 300€, l'assicurazione non paga nulla, e l'intero importo resta a tuo carico.Franchigia Relativa: Funziona come una soglia di sbarramento. Se il danno è pari o inferiore alla franchigia, l'assicurazione non paga nulla. Se invece il danno supera la franchigia, l'assicurazione ti rimborsa l'intero importo del danno, senza trattenere nulla.Esempio: Hai una franchigia relativa di 500€ e subisci un danno di 1.200€. L'assicurazione ti rimborsa tutti i 1.200€. Se il danno è di 300€, anche in questo caso l'assicurazione non paga nulla.In sintesi, la franchigia assoluta riduce sempre il risarcimento, mentre la franchigia relativa lo annulla solo per i danni di lieve entità, ma garantisce un rimborso totale per i danni più gravi.Puoi simulare tu stesso come cambia il risarcimento modificando i valori qui sotto:

**Evaluation**:
- **Correctness**: 2 (Fully correct)
- **Completeness**: 2 (Complete)
- **Grounding**: N/A
- **Citation**: N/A
- **Hallucinated?**: N
- **Notes**: Solid explanation with examples. The formatting is slightly compressed, but the content is technically sound.

---

## 4. NotebookLM

**Output**: N/A

**Evaluation**:
- **Correctness**: N/A
- **Completeness**: N/A
- **Grounding**: N/A
- **Citation**: N/A
- **Hallucinated?**: N/A
- **Notes**: N/A (Requires document upload)
