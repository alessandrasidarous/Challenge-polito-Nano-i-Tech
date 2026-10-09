# Evaluation for S-05: Limite aggregato, pluviale e 4° sinistro

**Scenario:** Tre sinistri da acqua già liquidati per 15.000€ nell'anno. Un quarto sinistro causato da un pluviale genera 10.000€ di danni. L'utente chiede di calcolare il residuo in base al "limite annuo aggregato" e di verificare lo scoperto per il "4° sinistro".

## Navisio AI

**Output Analysis:**
- Capisce correttamente che non esiste uno "scoperto progressivo" per il 4° sinistro, smontando un'altra trappola.
- Intuisce che il pluviale potrebbe rientrare nell'Acqua Piovana (Art. 2.3.4).
- **Errore di interpretazione sui limiti:** Applica il limite a scaglioni (10k, 20k, 50k) all'intera garanzia *Danni da Acqua*. Nel fascicolo, questo limite specifico (Art. 5.1) si applica solo alle spese accessorie di *ricerca e riparazione guasto*, mentre la garanzia base Danni da Acqua risarcisce fino alla Somma Assicurata del Fabbricato senza un limite annuo fisso di 10-50k.
- Fa comunque un ottimo ragionamento logico-matematico creando i tre scenari di "capienza residua", anche se basati su una premessa parzialmente inesatta.

**Scores:**
- **Correctness:** 1/2 (L'applicazione del limite aggregato 10k/20k/50k all'intera garanzia Danni da Acqua è errata, riguarda solo le spese di ricerca guasto).
- **Completeness:** 2/2 (Affronta tutti i punti: pluviale, scoperto progressivo, limiti aggregati e calcoli).
- **Grounding:** 2/2
- **Citation:** 2/2
- **Hallucination:** N

---

## NotebookLM

**Output Analysis:**
- **Lettura chirurgica del contratto:** NotebookLM coglie la grande trappola semantica. Il pluviale convoglia acqua meteorica, quindi **non è coperto** dalla garanzia "Danni da acqua" (che copre solo gli impianti idrici/riscaldamento). Viene espressamente escluso.
- Spiega che può essere coperto solo se c'è l'opzione "Acqua Piovana" (limite massimo 10.000€ annui).
- **Correzione sui limiti aggregati:** Smonta la premessa dell'utente chiarendo che per i normali Danni da Acqua *non c'è un limite annuo prefissato* (opera fino alla somma assicurata). Identifica correttamente che i limiti da 10k/20k/50k riguardano solo le garanzie accessorie (ricerca guasto).
- Conferma che non c'è scoperto progressivo per il 4° sinistro.
- Arriva alla conclusione esatta: se viene denunciato come danno da acqua è 0€. Se c'è acqua piovana è max 10.000€, a cui i 15.000€ precedenti (se liquidati come danni da acqua) non fanno cumulo perché appartengono a massimali diversi.

**Scores:**
- **Correctness:** 2/2
- **Completeness:** 2/2
- **Grounding:** 2/2
- **Citation:** 2/2 (via UI citation mechanism)
- **Hallucination:** N

---

## Confronto e Considerazioni

Questo test avanzato (`S-05`) misurava la capacità del modello di unire classificazione del sinistro (tubo idrico vs pluviale) e calcoli complessi (erosione del massimale aggregato).

**NotebookLM vince nettamente (8 vs 7)**. Ha dimostrato una capacità di analisi contrattuale superiore:
1. Ha colto che il pluviale è un'esclusione esplicita dei Danni da Acqua.
2. Ha corretto l'utente chiarendo che i Danni da Acqua non hanno un massimale aggregato di 10/20/50k (quelli sono solo per le ricerche guasto).

Navisio ha fatto un bel lavoro matematico creando gli scenari di erosione (15k su 20k = 5k residui), dimostrando buone capacità di ragionamento numerico, ma lo ha applicato al massimale sbagliato, confondendo la garanzia principale con la garanzia accessoria.

In questi test avanzati (Advanced Broker Claims), stiamo vedendo la differenza tra estrarre semplicemente del testo (dove Navisio è fortissimo) e comprendere l'architettura logica e gerarchica di un contratto di 100 pagine.
