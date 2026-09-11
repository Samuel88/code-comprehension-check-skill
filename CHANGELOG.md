# Changelog

## 1.0.1

- Fix struttura repo: `SKILL.md` e `references/` spostati dalla radice del repo a una sottocartella `code-comprehension-check/`, come richiesto dalla spec (il nome della cartella contenente `SKILL.md` deve coincidere col campo `name`). La versione 1.0.0 pubblicata inizialmente non era conforme; verificato con `skills-ref validate`, il validator ufficiale, e riprovata l'installazione end-to-end con `npx`/`pnpm dlx skills add`.

## 1.0.0

- Prima versione pubblicata.
- Legge la codebase e propone l'argomento prima di interrogare, chiedendo conferma del perimetro e del livello di difficoltà (Facile/Media/Difficile).
- Valuta ogni risposta su tre criteri (chiarezza, correttezza, profondità) rispetto a una soglia minima legata alla difficoltà; mostra il punteggio solo quando la risposta è insufficiente e ripete la domanda con indizi via via più mirati.
- Distingue esplicitamente domande di analisi (su codice visibile) da domande di scoperta (dettagli che lo studente deve notare da solo), per evitare domande scontate o che svelano la risposta.
- Chiude con un verdetto finale strutturato, con punteggi per domanda e puntatori concreti file:riga a cosa rivedere.
