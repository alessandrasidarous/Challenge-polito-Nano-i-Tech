# Evaluation: H-03

**Prompt**: "Qual è il massimale esatto in euro previsto dalla polizza per i danni da terrorismo?"
**Expected Answer**: "Not found" or "Massimale is chosen at signing, not present in this blank document"
**Category**: Hallucination, Reasoning
**Doc Used**: DOC-A (Unipol Condominio Più)

---

## 1. Navisio AI

**Output**: 
Il Set Informativo della polizza UnipolSai Condominio non indica una cifra in euro fissa e prestabilita per la copertura generale del terrorismo, ma definisce il massimale come percentuale della Somma Assicurata stabilita in polizza:
• Garanzia principale Fabbricato (Art. 2.3.5 - Atti vandalici e dolosi): il limite d'indennizzo per gli atti di terrorismo è pari al 50% della Somma Assicurata per il Fabbricato per ciascuna annualità assicurativa [1]. L'importo esatto in euro dipende quindi dal valore del fabbricato assicurato nel frontespizio di polizza.
• Danni estetici (imbrattamento e deturpamento delle parti esterne): la garanzia prevede un sottomassimale specifico fisso fino a 5.000,00 € per annualità assicurativa, con una franchigia di 250,00 € per sinistro [2].
• Impianti Solari e/o Fotovoltaici (Art. 2.3.8): anche per gli impianti la copertura per atti di terrorismo è prestata con il limite del 50% della Somma Assicurata dell'impianto per annualità assicurativa [3] (con uno scoperto del 20% e un minimo non indennizzabile di 1.500,00 €).

Fonti:
[1] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 37
[2] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 37
[3] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 38

**Evaluation**:
- **Correctness**: 2 (Correctly identified there is no exact euro amount for the general coverage)
- **Completeness**: 2 (Extracted the 50% rule perfectly)
- **Grounding**: 2 (Fully grounded in the document)
- **Citation**: 2 (Cited pages 37 and 38)
- **Hallucinated?**: N
- **Notes**: Excellent reasoning. Avoided the hallucination trap and explained the mechanism clearly.

---

## 2. Gemini Pro

**Output**: 
Nelle Condizioni di Assicurazione **non è indicato un massimale fisso espresso in euro** per i danni da terrorismo.

La polizza prevede invece un limite percentuale calcolato sulla somma assicurata pattuita nel singolo contratto:

* **Danni al Fabbricato (Garanzia Supplementare "Atti vandalici e dolosi" - Art. 2.3.5):** la copertura per gli Atti di terrorismo è prestata con il limite del **50% della Somma Assicurata per il Fabbricato** per ciascuna Annualità assicurativa.


* **Impianti solari e/o fotovoltaici (Garanzia Supplementare opzionale - Art. 2.3.8):** anche in questo caso i danni da atti di terrorismo sono coperti fino al **50% della Somma Assicurata** per tali impianti per ciascuna Annualità assicurativa.



L'importo esatto in euro corrisponde quindi alla metà (50%) della **Somma Assicurata per il Fabbricato** (e per gli impianti solari/fotovoltaici, se presenti) indicata specificamente nella Scheda di Polizza. Nelle altre sezioni della polizza (come il Contenuto delle singole unità immobiliari, la Tutela Legale e la Sezione Famiglie), gli atti di terrorismo sono espressamente esclusi.

**Evaluation**:
- **Correctness**: 2 (Correctly identified there is no exact euro amount)
- **Completeness**: 2 (Extracted the 50% rule)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 0 (Cited Art 2.3.5 but no pages)
- **Hallucinated?**: N
- **Notes**: Excellent reasoning. Avoided the hallucination trap.

---

## 3. DeepSeek

**Output**: 
In base alla documentazione fornita, il massimale esatto previsto per i danni da terrorismo varia a seconda della garanzia specifica attivata:

1.  **Per la Garanzia Supplementare "Atti vandalici e dolosi" (Sezione Danni ai Beni):**
    Il limite di indennizzo è pari al **50% della Somma Assicurata per il Fabbricato per Annualità assicurativa**.
    *(Riferimento: Pag. 37, Art. 2.3.5 e Pag. 41, tabella di sintesi)*

2.  **Per la Garanzia Supplementare "Impianti solari e/o fotovoltaici" (Sezione Danni ai Beni):**
    Il limite di indennizzo è pari al **50% della Somma Assicurata per Annualità assicurativa**.
    *(Riferimento: Pag. 38, Art. 2.3.8 e Pag. 42, tabella di sintesi)*

**Nota:** Nella tabella di sintesi a pagina 41, alla voce "Atti vandalici e dolosi", viene riportato esplicitamente: "Atti di terrorismo fino al 50% della Somma Assicurata per Annualità assicurativa".

**Evaluation**:
- **Correctness**: 2 (Correctly identified there is no exact euro amount, just 50%)
- **Completeness**: 2 (Extracted the 50% rule)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 2 (Cited exact pages 37, 38, 41, 42)
- **Hallucinated?**: N
- **Notes**: Excellent retrieval and reasoning. Great citation of the summary tables too.

---

## 4. NotebookLM

**Output**: 
Nel documento contrattuale **non è indicato un massimale fisso espresso in euro** per i danni da terrorismo. 

La polizza prevede invece un limite percentuale calcolato sulla somma assicurata concordata nel singolo contratto:

* **Esclusione nella Garanzia Base**: i danni provocati da atti di terrorismo sono esclusi dalle coperture base della sezione Danni ai Beni.
* **Garanzia supplementare "Atti vandalici e dolosi" (Art. 2.3.5)**: se attivata a pagamento, copre i danni materiali e diretti causati da atti dolosi di terzi, compresi quelli di terrorismo. Per gli **Atti di terrorismo**, la garanzia opera con il limite del **50% della Somma Assicurata per il Fabbricato per Annualità assicurativa**. L'importo monetario esatto dipende quindi dal valore complessivo assicurato per l'edificio riportato nella scheda di polizza.
* **Impianti solari e/o fotovoltaici (Art. 2.3.8)**: se viene acquistata la relativa garanzia supplementare, i danni da atti di terrorismo a tali impianti sono anch'essi indennizzabili fino al **50% della Somma Assicurata** specifica per gli impianti stessi per ciascuna annualità.

Per la garanzia "Atti vandalici e dolosi", la liquidazione prevede l'applicazione di uno **scoperto del 10% con un minimo di 100 €**, oppure **nessuno scoperto/franchigia**, a seconda dell'opzione sottoscritta in polizza.

🏢 Vuoi verificare anche le franchigie o le condizioni previste per altre garanzie opzionali, come gli eventi catastrofali o gli atti vandalici comuni? (citazioni tramite ui)

**Evaluation**:
- **Correctness**: 2 (Correctly identified there is no exact euro amount)
- **Completeness**: 2 (Extracted the 50% rule and deductibles)
- **Grounding**: 2 (Fully grounded)
- **Citation**: 2 (Exact UI citations)
- **Hallucinated?**: N
- **Notes**: Excellent reasoning and extraction.
