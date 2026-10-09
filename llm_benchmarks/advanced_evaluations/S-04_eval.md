# Evaluation for S-04: Danni da acqua e rottura tubazioni (Ricerca guasto)

**Scenario:** Sinistro da acqua condotta con tre voci di spesa distinte: danno al muro (2.000€), spese ricerca guasto/rottura (1.500€), fattura idraulico per il tubo (300€). Viene posta la domanda specifica "Il tubo rotto viene pagato?", che in ambito assicurativo rappresenta un classico trick (solitamente la tubazione che origina il danno è esclusa).

## Navisio AI

**Output Analysis:**
- Risponde correttamente che **tutte e tre le voci** sono indennizzabili.
- Affronta brillantemente il "trick" sul tubo: sottolinea esplicitamente che, a differenza delle polizze standard, l'Art. 5.1 di questa specifica polizza (Unipol) paga anche la riparazione/sostituzione del tubo rotto. Estrazione perfetta della clausola.
- Menziona i presupposti (rottura accidentale, non degrado).
- Menziona genericamente l'applicazione di un "sottomassimale" senza però specificarne gli importi previsti dal contratto.

**Scores:**
- **Correctness:** 2/2
- **Completeness:** 1/2 (Estrazione perfetta delle coperture, ma manca l'estrazione quantitativa del limite del sottomassimale per la ricerca guasto)
- **Grounding:** 2/2
- **Citation:** 2/2
- **Hallucination:** N

---

## NotebookLM

**Output Analysis:**
- Stessa ottima interpretazione sulle 3 voci, incluso il recupero esatto della clausola che deroga lo standard di mercato e paga il tubo guasto.
- Va molto oltre nell'estrazione: recupera esattamente i **limiti quantitativi** del sottomassimale cumulativo per ricerca e riparazione (1% della Somma Assicurata, massimali a scelta di 10.000€, 20.000€ o 50.000€) dimostrando che la spesa di 1.800€ è capiente.
- Menziona l'opzione "Riparazione Diretta" (UnipolHome) come servizio aggiuntivo.

**Scores:**
- **Correctness:** 2/2
- **Completeness:** 2/2 (Eccezionale livello di dettaglio quantitativo)
- **Grounding:** 2/2
- **Citation:** 2/2 (via UI citation mechanism)
- **Hallucination:** N

---

## Confronto e Considerazioni

Il prompt conteneva un test sulla comprensione profonda delle differenze contrattuali rispetto agli standard di mercato: nella maggior parte delle polizze, il "pezzo guasto" (il tubo) non viene pagato, ma si pagano solo ricerca guasto e danni da bagnamento. **Entrambi i modelli hanno estratto la regola corretta specifica per il documento in esame**, superando il rischio di allucinazione basata sulla conoscenza pregressa di settore.

**NotebookLM vince sulla Completezza (2 vs 1):** oltre a dire *cosa* viene pagato, estrae anche il limite di *quanto* viene pagato, trovando il sottomassimale percentuale (1%) e le opzioni assolute (10k/20k/50k) dal Fascicolo. Navisio si è limitato ad un'estrazione qualitativa.
