# Navisio AI — Analisi Benchmark & Strategia Challenge PoliTo

> Benchmark condotto su 4 modelli: **Navisio AI**, **NotebookLM**, DeepSeek, Gemini Pro.
> 34 test cases: Knowledge Base, Document QA (Shallow + Deep), Hallucination Resistance,
> Document Comparison, Contradictory Reasoning, Claims Analysis.

---

## Risultati Globali

| Modello | Overall Score | Allucinazioni |
|-------|:------------:|:--------------:|
| NotebookLM | **100%** | 0 |
| **Navisio AI** | **96%** | 1 |
| DeepSeek | 88% | 0 |
| Gemini Pro | 83% | 0 |

Navisio è **4 punti dietro NotebookLM** nel punteggio globale. Questo divario è minimo in aggregato, ma è concentrato in una singola sezione: **Claims Analysis (79% vs. 100%)**, dove si sono verificati tutti e tre gli errori di Navisio. Ogni altra sezione si attesta al 97–100%.

---

## Sezione per Sezione: Navisio vs. NotebookLM

| Sezione | Navisio AI | NotebookLM | Gap | Dove Navisio ha perso punti |
|---------|:----------:|:----------:|:---:|--------------------------|
| Knowledge Base | 92% | N/A | — | K-01: nessuna citazione (N/A by design) |
| Doc QA Shallow | 100% | 100% | 0 | Nessuno |
| Doc QA Deep | 100% | 100% | 0 | Nessuno |
| Hallucination Resistance | 100% | 100% | 0 | Nessuno |
| Document Comparison | 97% | 100% | -3% | C-03: mancata sfumatura opzionale vs. automatico |
| Contradictory Info | 100% | 100% | 0 | Nessuno |
| **Claims Analysis** | **79%** | **100%** | **-21%** | S-01: procedura omessa; S-02: tempistica errata; S-03: allucinazione |

**Il gap globale di 4 punti è quasi interamente spiegato dalla Claims Analysis.** Se le performance sui sinistri avessero eguagliato NotebookLM, il punteggio globale di Navisio sarebbe stato ~99.5%.

---

## Punti di Forza di Navisio (Sintesi)

Questi punti sono solidi e ben differenziati da tutti i competitor:

- **Citazione normativa**: L'unico modello a citare IVASS, articoli del CAP e del Codice Civile con link verificati a Normattiva.it. NotebookLM non può farlo (nessuna KB, nessuna integrazione normativa).
- **Citazione esatta della pagina sui documenti**: Un costante 2.0/2 in tutti i test documentali. Gemini Pro: 0.3/2.
- **Accuratezza della KB proprietaria**: L'unico modello con i limiti corretti per la RC Auto in K-06. DeepSeek ha fornito valori obsoleti.
- **Confronto multi-documento**: 97% con correttezza totale; Gemini Pro ha fallito C-04 completamente (0/8).
- **Ragionamento su clausole contraddittorie**: 100%, a pari merito solo con NotebookLM.

Questi punti di forza sono le fondamenta del pitch per la challenge. Il resto di questo report si concentra sul gap.

---

## Analisi del Gap: Dove NotebookLM ha superato Navisio

### GAP 1 — Claims Analysis: Procedura vs. Quadro Legale (Test S-01, S-02)

**Cosa è successo**: In S-01 (incendio appartamento, impianto elettrico non a norma), Navisio ha prodotto un'eccellente analisi legale — citando gli Artt. 1892, 1893, 1898, 1900 del Codice Civile — ma non ha estratto gli step operativi concreti dal documento di polizza caricato:
- **Non** ha menzionato la scadenza di 10 giorni per la denuncia (Art. 9.1 Unipol)
- **Non** ha menzionato il diritto a richiedere un anticipo del 50% per danni oltre €30.000
- **Non** ha menzionato il limite di 30 giorni per la conservazione delle prove fisiche

In S-02 (furto di gioielli, finestra rotta), Navisio ha citato l'Art. 1913 CC (default di 3 giorni) invece di leggere il termine contrattuale di 10 giorni — affidandosi a un default legale generale quando il documento forniva una regola specifica e più favorevole.

**L'approccio di NotebookLM**: Ha invertito la priorità — ha controllato prima il documento, estratto la checklist operativa, e poi aggiunto le disposizioni del Codice Civile come contesto supplementare.

**Root cause**: La pipeline di ragionamento di Navisio sembra dare maggiore peso alla conoscenza normativa (Codice Civile, IVASS) rispetto all'estrazione specifica dal documento negli scenari di sinistro. Il modello attinge prima alla sua KB e usa il documento per confermare, invece di leggere prima il documento e usare la KB per integrare.

**Proposta di miglioramento**:

> **Implementare una "Claims Mode" con gerarchia delle fonti applicata.**
>
> Quando una query è classificata come richiesta di gestione sinistro (keyword: sinistro, denuncia, danno, indennizzo, rimborso), applicare un ordine di ragionamento fisso:
> 1. Estrarre tutte le clausole rilevanti dal documento caricato (tempistiche, obblighi, soglie di anticipo, requisiti di prova)
> 2. Applicare il Codice Civile solo dove il documento è silente
> 3. Strutturare l'output come: **Checklist Operativa (con scadenze)** prima, poi Analisi Legale in secondo piano
>
> Risultato atteso: elimina i due fallimenti di grounding in S-01 e S-02, portando la Claims Analysis dal 79% al ~95%.

---

### GAP 2 — Premise Verification: Allucinazione da Falso Input Utente (Test S-03)

**Cosa è successo**: L'utente ha chiesto: *"La polizza prevede denuncia entro 30 giorni dalla scoperta. Sono ancora in tempo?"* L'attuale polizza Unipol richiede la denuncia entro **10 giorni**. Navisio ha accettato la premessa dei 30 giorni come vera e ha risposto di conseguenza — producendo una risposta legalmente errata con alta sicurezza e citazioni precise del Codice Civile (Artt. 1913, 1915).

Questa è **l'unica allucinazione** di Navisio in 34 test, ma è strutturalmente significativa: l'errore non è stato causato da una mancanza di informazioni, ma dal fidarsi dell'utente più del documento.

**L'approccio di NotebookLM**: Ha immediatamente segnalato la discrepanza: *"La tua premessa contiene una discrepanza con i termini contrattuali — la polizza stabilisce 10 giorni, non 30."* Ha poi risposto alla vera domanda E ha aggiunto la rete di salvataggio legale dell'Art. 1915 (denuncia tardiva ≠ perdita automatica della copertura se non c'è dolo).

**Root cause**: Navisio attualmente non applica uno step di **premise verification** prima di rispondere. Quando l'utente formula un'asserzione fattuale come precondizione, il modello l'accetta senza verificarla rispetto al documento caricato.

**Proposta di miglioramento**:

> **Aggiungere un layer di Premise Verification alla pipeline RAG.**
>
> Prima di generare una risposta, estrarre eventuali asserzioni fattuali dal prompt dell'utente (date, importi, tempistiche, condizioni) ed eseguire una ricerca di similarità sul documento indicizzato. Se l'asserzione contraddice il documento con alta confidenza, iniettare un prefisso di correzione nella risposta:
>
> *"Nota: la polizza caricata specifica [X], non [Y] come indicato nella tua domanda. Rispondo in base al documento:"*
>
> Questo non è un rifiuto — è una correzione. La risposta continua, ma fondata sulle giuste informazioni.
>
> Risultato atteso: elimina l'allucinazione in S-03 e trasforma il fallimento in una feature differenziante: *"Navisio ti corregge quando la tua premessa è sbagliata — gli altri modelli ti assecondano."*

---

### GAP 3 — Profondità Strutturale nel Confronto Multi-Documento (Test C-03)

**Cosa è successo**: In C-03 (confronto RCO tra AIG e AXA), Navisio ha descritto correttamente cosa coprono entrambe le polizze ma ha mancato la distinzione strutturalmente critica: nella polizza AXA, la RCO è **inclusa automaticamente** nella copertura base; nella polizza AIG, è un **add-on opzionale** che richiede un'attivazione esplicita. Questa distinzione ha implicazioni dirette sul premio e sulla copertura.

**L'approccio di NotebookLM**: Ha aggiunto una dimensione strutturale esplicita — etichettando ciascuna copertura come "incluso automaticamente" vs "opzionale su richiesta", e annotandone la conseguenza: un assicurato che dimentica di attivare l'opzione è scoperto.

**Root cause**: La logica di confronto di Navisio opera a livello di *contenuto* ("X è coperto?") ma non a livello *strutturale* ("come viene attivato X?", "a che costo?", "di default o per scelta?"). Questo è un gap nel template del prompt di confronto, non nel modello sottostante.

**Proposta di miglioramento**:

> **Aggiungere dimensioni di metadati strutturali allo schema di output del confronto.**
>
> Per ogni copertura identificata in un confronto multi-documento, richiedere al modello di popolare:
> - **Attivazione**: automatica / opzionale / condizionata
> - **Costo**: incluso nel premio base / premio aggiuntivo
> - **Trigger**: sempre attivo / richiede sinistro esplicito / richiede dichiarazione preventiva
>
> Questo può essere implementato tramite prompt engineering (schema di output) o tramite uno step di estrazione strutturata prima della sintesi del confronto.
>
> Risultato atteso: colma il gap in C-03 e aumenta sostanzialmente il valore commerciale della feature di confronto — il broker può vedere a colpo d'occhio quali coperture richiedono un'azione da parte del cliente.

---

### GAP 4 — Formato Output Sinistri: Memo Legale vs. Checklist Operativa

**Cosa è successo** (tutti i test S): Le risposte ai sinistri di Navisio sono scritte come memo legali professionali — profonde, accurate, ben citate — ma organizzate attorno a categorie legali (quale clausola si applica, cosa dice la legge) piuttosto che attorno a cosa il cliente deve fare e quando.

NotebookLM ha costantemente strutturato le sue risposte ai sinistri come:
1. **Azioni immediate** (mettere in sicurezza i locali, chiamare i pompieri, conservare le prove)
2. **Obblighi di denuncia** (chi avvisare, come, entro quale scadenza)
3. **Gestione finanziaria** (diritti all'anticipo, processo di liquidazione, tempistiche di pagamento)
4. **Sfumature legali** (fallback del Codice Civile, cosa succede in caso di ritardo)

Navisio ha fatto l'opposto: sfumature legali per prime, checklist operativa per ultima o mai.

**Proposta di miglioramento**:

> **Forzare un template di output standard per la Claims Analysis mode.**
>
> ```
> ## Sintesi Sinistro
> [Verdetto in una riga: coperto / non coperto / condizionato]
>
> ## Azioni Immediate
> - [ ] [Azione] — scadenza: [X giorni dall'evento/scoperta]
> - [ ] [Azione]
>
> ## A Cosa Hai Diritto
> - Anticipo: [Y%] se danno > [€Z] (Art. X.X)
> - Riparazione: [diretta / standard / non disponibile]
>
> ## Note Legali e Contrattuali
> [Codice Civile, esclusioni, casi limite]
> ```
>
> Questo template può essere implementato come estensione del system prompt per la funzionalità Claims Analysis — non è necessario alcun fine-tuning del modello, solo prompt engineering.

---

### GAP 5 — Completezza sui Costi Accessori e Sub-Limiti (Test CR-02, S-01)

**Cosa è successo**: In diversi test, Navisio ha identificato correttamente il limite principale o la copertura ma ha omesso i sub-limiti accessori che spesso sono altrettanto importanti nella pratica:
- CR-02: ha trovato correttamente il limite terremoto a livelli 50/70/100% ma (nel primo passaggio) non ha fatto emergere il sub-limite per demolizione/sgombero (10% dell'indennizzo, max €20.000) o il cap per riprogettazione/direzione lavori (€5.000)
- S-01: non ha menzionato la copertura dei costi accessori per lo sgombero delle macerie (20% dell'indennizzo, max €100.000) o le opere provvisionali (20%, max €50.000)

NotebookLM ha recuperato tutti i limiti accessori senza essere sollecitato in entrambi i test.

**Root cause**: Lo step di retrieval del modello recupera probabilmente i chunk semanticamente più rilevanti (clausola principale di copertura) senza scansionare esaustivamente le sotto-clausole e i limiti accessori nei paragrafi adiacenti.

**Proposta di miglioramento**:

> **Implementare una "completeness sweep" per i limiti finanziari.**
>
> Dopo che la risposta principale è stata generata, eseguire un secondo passaggio di retrieval mirando specificamente a: limiti monetari, sub-limiti, cap, franchigie e scoperti adiacenti ai chunk recuperati. Se ne vengono trovati, aggiungerli alla risposta in una sezione dedicata "Limiti e Sub-limiti".
>
> Questo rispecchia come un perito esperto legge una polizza: trova la clausola principale, poi esamina gli articoli circostanti per eventuali limiti modificanti.

---

### GAP 6 — Nessuna Analisi delle Conseguenze ex Art. 1915 nei Sinistri (Test S-03)

**Cosa è successo**: In S-03 (denuncia di sinistro tardiva), sia DeepSeek che Gemini Pro hanno identificato la regola corretta dei 10 giorni ma si sono fermati lì. Navisio ha avuto un'allucinazione. Fondamentalmente, **solo NotebookLM** ha aggiunto la rete di sicurezza legalmente essenziale: in base all'Art. 1915 CC, una denuncia tardiva non annulla automaticamente la copertura — l'assicuratore può solo ridurre l'indennizzo in proporzione al pregiudizio effettivo subito, e solo se il ritardo era colposo (non doloso).

Questa è esattamente l'informazione di cui un cliente in questa situazione ha più bisogno: *"Sì, hai mancato la scadenza — ma non sei necessariamente scoperto."*

**Proposta di miglioramento**:

> **Aggiungere un blocco di "Consequence Analysis" alle query relative alle scadenze.**
>
> Ogni volta che una risposta coinvolge una scadenza procedurale (denuncia, conservazione delle prove), aggiungere automaticamente:
> - Cosa succede se la scadenza non viene rispettata (riduzione proporzionale vs decadenza totale)
> - A quali condizioni è applicabile la decadenza (dolo vs colpa)
> - Se il cliente ha ancora un ricorso
>
> Si tratta di un'informazione ad alto valore aggiunto che riduce l'ansia del cliente e dimostra profondità legale — esattamente dove uno strumento verticale come Navisio dovrebbe superare un modello generico.

---

## Classifica di Priorità dei Miglioramenti

| # | Miglioramento | Effort | Impatto | Test Risolti |
|---|------------|:------:|:------:|-------------|
| 1 | Claims Mode: gerarchia fonti forzata (contratto > legge) | Medio | Alto | S-01, S-02 |
| 2 | Layer di Premise Verification | Medio | Alto | S-03 |
| 3 | Blocco Consequence Analysis per scadenze | Basso | Alto | S-03 |
| 4 | Template output Claims standardizzato | Basso | Medio | S-01, S-02, S-03 |
| 5 | Metadati strutturali nei confronti | Basso | Medio | C-03 |
| 6 | Completeness sweep per limiti accessori | Medio | Medio | CR-02, S-01 |

Gli elementi 3 e 4 sono **solo prompt engineering** — nessuna modifica al modello richiesta, implementabili immediatamente.
Gli elementi 1, 2, 5, 6 richiedono aggiustamenti alla pipeline RAG o al retrieval.

---

## Framing Conclusivo per la Challenge

```
Navisio e NotebookLM hanno pareggiato in 6 sezioni di test su 7.
L'intero divario è concentrato nella Claims Analysis.

La causa principale non è un problema di conoscenza — è un problema di
priorità di ragionamento: Navisio attinge prima alla sua KB normativa
e legge il documento per secondo, mentre per le query operative dovrebbe essere l'opposto.

La soluzione è architetturale, non richiede un riaddestramento (retrain):
  → Gerarchia delle fonti nella Claims Mode
  → Premise verification prima di rispondere
  → Template di output forzato

Con queste tre modifiche, Navisio chiude il gap con NotebookLM
mantenendo i suoi vantaggi unici:
  → KB normativa in tempo reale (NotebookLM non ne ha)
  → Citazioni esatte della pagina
  → Database di prodotti proprietario
```

---

*Benchmark condotto: 2026-10-07 to 2026-10-09*
*Autore: Alessandro — Challenge @ PoliTo Nano-i-Tech*
