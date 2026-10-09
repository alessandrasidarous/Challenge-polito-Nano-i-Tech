# Evaluation: CR-02

**Prompt**: "Qual è il massimale in caso di terremoto?"
**Expected Answer**: Identify the specific sub-limits and percentage structures for earthquake coverage (overriding standard limits).
**Category**: Complex reasoning, Calculation
**Docs Used**: DOC-A (Unipol Condominio Più)

*Note: The hypothetical numbers in the testing protocol ("20% of 500,000") were placeholders. The actual policy dictates 50%, 70%, or 100% of the insured sum.*

---

## 1. Navisio AI

**Output**: 
Nel Set Informativo UnipolSai Condominio Più (Sezione Eventi Catastrofali), il massimale per la garanzia Terremoto è espresso come percentuale della Somma Assicurata ed è condizionato dalla scelta indicata in Polizza:
• Massimale / Limite di indennizzo: A seconda dell'opzione selezionata dal Contraente nel frontespizio/scheda di polizza, l'indennizzo è prestato fino al raggiungimento del 50%, 70% oppure 100% della Somma Assicurata per il Fabbricato per ciascuna annualità assicurativa [1].
• Scoperto e Minimo non indennizzabile: Per ciascun sinistro si applica uno scoperto del 10% sull'importo del danno, con un minimo non indennizzabile di 20.000,00 € [2].

Limiti per Spese Accessorie e Aggiuntive [1]
All'interno della garanzia sono inoltre previsti i seguenti limiti specifici:
• Demolizione, sgombero e trasporto residui: Fino al 10% dell'indennizzo, con un massimo di 20.000,00 €.
• Riprogettazione, direzione lavori e oneri di ricostruzione: Massimo 5.000,00 €.
• Opere provvisionali di cantiere: Fino al 10% dell'indennizzo, con un massimo di 20.000,00 €.

Fonti:
[1] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 50
[2] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 51

**Evaluation**:
- **Correctness**: 2 (Correctly extracted the real policy limits)
- **Completeness**: 2 (Included the base limits, deductibles, and accessory limits)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 2 (Exact page citations)
- **Hallucinated?**: N
- **Notes**: Perfect extraction of the tiered percentage system and sub-limits.

---

## 2. DeepSeek

**Output**: 
In base alla documentazione fornita, per la garanzia **Terremoto** (che fa parte della Sezione Eventi Catastrofali), il massimale non è un importo fisso, ma dipende dalla scelta effettuata dal Contraente al momento della stipula della polizza.
[... lists 50%, 70%, 100% and Art. 4.1.2 pag. 50 ...]
Inoltre, è previsto uno **Scoperto del 10%** del danno, con un **minimo non indennizzabile di € 20.000,00** (Art. 4.1.4 - Scoperti, pag. 51 del PDF).

**Evaluation**:
- **Correctness**: 2 (Correctly identified the structure)
- **Completeness**: 1 (Missed the accessory limits like demolition and provisional works that the others caught)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 2 (Successfully cited exact articles and page numbers!)
- **Hallucinated?**: N
- **Notes**: Great job citing specific pages this time, but slightly less complete than the others regarding sub-limits.

---

## 3. NotebookLM

**Output**: 
Per la garanzia **Terremoto** (Sezione Eventi Catastrofali), il limite massimo indennizzabile per i danni materiali e diretti al Fabbricato viene stabilito in base alla scelta effettuata dal Contraente e indicata nel contratto. 
[... lists 50%, 70%, 100% ...]
### Sottolimiti per spese accessorie
[... lists the 3 sub-limits ...]
### Scoperti applicabili
[... lists the 10% and €20k ...]

**Evaluation**:
- **Correctness**: 2 (Correct)
- **Completeness**: 2 (Caught everything)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 2 (UI citations)
- **Hallucinated?**: N
- **Notes**: Excellent extraction.

---

## 4. Gemini Pro

**Output**: 
Nella polizza **Unipol Condominio Più** (Sezione Eventi Catastrofali - Terremoto), il massimale (limite di indennizzo) non è una cifra fissa prestabilita, ma viene definito in sede di contratto in percentuale rispetto alla **Somma Assicurata per il Fabbricato**.
[... lists 50%, 70%, 100% ...]
### Sottolimiti e Spese Accessorie Garantite
[... lists the 3 sub-limits ...]
### Scoperto e Minimo Non Indennizzabile
[... lists the 10% and €20k ...]

**Evaluation**:
- **Correctness**: 2 (Correct)
- **Completeness**: 2 (Caught everything)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 0 (No specific articles or pages cited)
- **Hallucinated?**: N
- **Notes**: Excellent data extraction, though as usual, lacking precise citations.
