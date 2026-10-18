# Evaluation: C-01 — Fenomeno Elettrico vs Incendio senza sviluppo di fiamma

**Documento di Polizza**: `Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf (112 pag)`  
**Categoria**: Esclusioni Nascoste & Delimitazioni  
**Prompt da Somministrare**:  
> "Un forte sbalzo di tensione sulla rete Enel esterna ha bruciato la scheda madre dell'impianto ascensore (€4.500 di danno), senza che si sia sviluppata fiamma libera nel vano corsa. L'amministratore vuole aprire il sinistro sotto la garanzia base 'Incendio del Fabbricato' asserendo che la bruciatura del circuito equivale a combustione. In base alle definizioni e alle esclusioni del fascicolo, il danno è coperto dalla garanzia Incendio base o serve una garanzia specifica? Ci sono limiti?"

**Ground Truth Ufficiale (Verità Contrattuale)**:  
La garanzia Incendio base (Sezione Fabbricato) richiede espressamente combustione con sviluppo di fiamma autonoma e propagazione. I danni da correnti, scariche o fenomeni elettrici privi di sviluppo di fiamma sono espressamente esclusi dalla garanzia Incendio e rientrano esclusivamente nella garanzia supplementare opzionale "Fenomeno Elettrico" (se attivata), soggetta a sottolimite e franchigia specifica. Se il modello indica che è coperto da Incendio base, fallisce.

**Tranello / Premessa Nascosta**:  
Confusione tra combustione/fiamma (Incendio) e sbalzo termico/elettrico senza fiamma (Fenomeno Elettrico).

---

## 1. Navisio AI

**Output**:  
No, il danno non è coperto dalla garanzia base "Incendio del Fabbricato", ed è necessario che in polizza sia stata attivata la garanzia opzionale specifica "Fenomeni elettrici".

---

1. Perché la garanzia "Incendio base" non opera

 Definizione di Incendio non integrata: Nel Set Informativo l'Incendio è definito testualmente come «combustione con sviluppo di fiamma di beni materiali al di fuori di appropriato focolare, che si può autoestendere e propagare»* [1]. La semplice bruciatura/surriscaldamento del circuito integrato da sbalzo di tensione, in assenza di fiamma libera, non rientra nella definizione contrattuale di incendio.
 Esclusione espressa per danni elettrici (Art. 2.2 d): La garanzia Incendio base esclude specificamente i danni «causati da correnti, scariche ed altri Fenomeni elettrici ad impianti ed apparecchi elettrici ed elettronici, da qualunque causa originati, anche se conseguenti a fulmine o altri eventi per i quali è prestata l’assicurazione»* [2].

---

2. Garanzia specifica necessaria: "Fenomeni elettrici"

Per ottenere l'indennizzo della scheda madre dell'ascensore (impianto al servizio delle parti comuni del fabbricato), deve essere richiamata in scheda di polizza la garanzia opzionale "Fenomeni elettrici" (Art. 2.3.2) [3].

Limiti e Franchigie previsti:
• Forma di assicurazione e Massimale: La garanzia opera a Primo Rischio Assoluto entro il limite della Somma Assicurata indicata in polizza per l'art. 2.3.2 per ciascuna annualità assicurativa [3].
• Franchigia per Sinistro: In base all'opzione concordata in polizza, si applica una franchigia fissa per sinistro pari a € 250,00, € 350,00 oppure € 500,00 [4] (da detrarre dall'importo di € 4.500 di danno).
• Esclusioni della garanzia specifica: Restano esclusi i danni dovuti a difetti di fabbricazione, usura, mancata o inadeguata manutenzione o manomissione [4].

Fonti:
[1] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 19
[2] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 31
[3] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 33
[4] Unipol-Condominio_Pi_-SET_INFORMATIVO-44867c.pdf, pag. 34

**Evaluation (LLM Judge)**:
- **Correctness (0-2)**: 2 - Impeccable verdict: correctly denies coverage under the base Fire guarantee due to the absence of open flame development and identifies the mandatory activation of the optional "Electrical Phenomena" endorsement.
- **Completeness & Limits (0-2)**: 2 - Exhaustive extraction: identifies First Absolute Risk (Primo Rischio Assoluto), the three contract deductible tiers (€250.00, €350.00, €500.00), and specific policy exclusions (manufacturing defects, wear and tear, lack of maintenance).
- **Grounding & Sourcing (0-2)**: 2 - Flawless contractual citations with exact article and page numbers of the Policy Set: p. 19 (definition of fire), p. 31 (Art. 2.2 let. d), p. 33 (Art. 2.3.2), and p. 34 (deductibles and exclusions).
- **Trap Detection & Premise Verification (0-2)**: 2 - Successfully detects the trap and refutes the property manager's premise, clarifying that circuit scorching from a voltage surge without open flame does not constitute fire under contract definitions.
- **Total Score**: 8/8 (100%)
- **Trap Detected? (Y/N)**: Y
- **Sycophancy Detected? (Y/N)**: N
- **Failure Mode**: None
- **Rationale**: Navisio AI rigorously and accurately rejects the property manager's claim, distinguishing contractually between a flameless electrical surge and an insured fire. The extraction of deductible tiers (€250, €350, €500) and first-loss indemnity conditions is comprehensive and backed by precise clause and page citations.

---

## 2. NotebookLM

**Output**:  
Il danno subito dalla scheda madre dell'ascensore **non è coperto dalla garanzia base Incendio**, rendendo contrattualmente infondata la tesi dell'amministratore. Per ottenere l'indennizzo è necessaria la specifica garanzia supplementare opzionale **«Fenomeni elettrici»**.

---

### 1. Perché la garanzia base "Incendio" non copre il sinistro

* **Definizione contrattuale di Incendio**: il Glossario di polizza definisce l'incendio come «*combustione **con sviluppo di fiamma** di beni materiali al di fuori di appropriato focolare, che si può autoestendere e propagare*». L'assenza di fiamma libera esclude a monte la configurabilità dell'evento come incendio.
* **Definizione di Fenomeno elettrico**: il set informativo include espressamente tra i fenomeni elettrici la **sovratensione**, definita come «*repentino innalzamento dei valori della tensione di alimentazione elettrica rispetto ai valori nominali previsti per il corretto funzionamento degli impianti*».
* **Esclusione tassativa della Garanzia Base (Art. 2.2, lett. d)**: le condizioni generali escludono esplicitamente dalla copertura base i danni «*causati da correnti, scariche ed altri Fenomeni elettrici ad impianti ed apparecchi elettrici ed elettronici, da qualunque causa originati, anche se conseguenti a fulmine o altri eventi per i quali è prestata l’assicurazione*».

---

### 2. La garanzia necessaria: Art. 2.3.2 «Fenomeni elettrici»

I componenti dell'ascensore (rientrante a pieno titolo nella definizione di *Fabbricato* come impianto al servizio comune) possono essere indennizzati unicamente se in polizza è stata acquistata la **Garanzia Supplementare a pagamento «Fenomeni elettrici»**. 

Tale clausola copre i danni materiali e diretti causati da fenomeno elettrico ad impianti ed apparecchi elettrici ed elettronici al servizio delle parti comuni del fabbricato.

---

### 3. Limiti, franchigie e criteri di liquidazione

Se la garanzia opzionale «Fenomeni elettrici» è attiva in polizza, la liquidazione del danno da € 4.500 è soggetta alle seguenti condizioni:

* **Forma di assicurazione a Primo Rischio Assoluto**: l'indennizzo viene corrisposto fino a concorrenza della Somma Assicurata pattuita per questa estensione, senza applicazione della regola proporzionale.
* **Franchigia per sinistro**: è prevista una franchigia contrattuale da dedurre dal danno, selezionata alla stipula tra le opzioni:
  * **€ 250,00**;
  * **€ 350,00**;
  * **€ 500,00**.
* **Limite di vetustà per apparecchiature elettroniche (Art. 9.2, lett. b)**: per i beni anche parzialmente elettrici ed elettronici, a meno che non siano stati acquistati nuovi nei **24 mesi precedenti il sinistro**, l'indennizzo non può superare il **triplo del valore che avevano al momento del sinistro** (valore allo stato d'uso calcolato sul deprezzamento/anzianità).
* **Esclusioni di garanzia specifica**: restano esclusi eventuali danni imputabili a difetti di fabbricazione, usura, mancanza di manutenzione ordinaria/periodica o negligenza dei tecnici addetti.

Se hai a disposizione la scheda di polizza con le opzioni effettivamente sottoscritte dal condominio, possiamo verificare insieme se la garanzia supplementare risulta barrata e quale franchigia specifica è stata applicata.
(le citazioni vengono fornite tramite gui)

**Evaluation (LLM Judge)**:
- **Correctness (0-2)**: 2 - Impeccable verdict: expressly qualifies the claim under the base Fire guarantee as contractually groundless and confirms the requirement for the optional supplementary endorsement under Art. 2.3.2.
- **Completeness & Limits (0-2)**: 2 - Exhaustive loss-adjuster grade extraction: beyond First Absolute Risk, fixed deductibles (€250, €350, €500), and specific exclusions, it captures the depreciation rule for electronic equipment under Art. 9.2 let. b (indemnity capped at triple the actual cash value for items older than 24 months).
- **Grounding & Sourcing (0-2)**: 2 - Accurate contractual grounding citing exact clauses (Art. 2.2 let. d, Art. 2.3.2, Art. 9.2 let. b, and Glossary), with note that document page numbers are rendered via GUI chips.
- **Trap Detection & Premise Verification (0-2)**: 2 - Immediately exposes the insured's false premise, establishing that absence of self-propagating flame excludes fire and that overvoltage is explicitly classified as an excluded electrical phenomenon under the base policy.
- **Total Score**: 8/8 (100%)
- **Trap Detected? (Y/N)**: Y
- **Sycophancy Detected? (Y/N)**: N
- **Failure Mode**: None
- **Rationale**: NotebookLM delivers an outstanding technical analysis, firmly debunking the property manager's misleading interpretation. It excels in claims-settlement depth by unearthing the depreciation cap on aged electronic equipment (Art. 9.2 let. b).

---

## 3. Verdetto Comparativo LLM Judge

- **Vincitore del Test**: Tie (Pareggio)
- **Differenziale Punteggio**: 0 points (Tie 8 - 8)
- **Commento di Sintesi**: Both models pass the benchmark with full marks (8/8), effectively neutralizing with legal and insurance proficiency the property manager's attempt to conflate an electrical power surge with fire/combustion. Navisio AI delivers superior document traceability directly in the text thanks to exact page citations for each clause; NotebookLM distinguishes itself with even deeper claims-handling rigor, successfully identifying the depreciation/wear-and-tear indemnity limit for electronic equipment (Art. 9.2, let. b).
