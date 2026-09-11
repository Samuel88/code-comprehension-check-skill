# code-comprehension-check

Agent Skill conforme allo standard [agentskills.io](https://agentskills.io/specification): interroga uno studente su una codebase reale con domande mirate a file/funzioni/logica effettivamente presenti, non un quiz teorico. Vedi [`code-comprehension-check/SKILL.md`](code-comprehension-check/SKILL.md) per le istruzioni complete.

## Installazione

```bash
npx skills add Samuel88/code-comprehension-check-skill -a <agente> -y --copy
# oppure con pnpm:
pnpm dlx skills add Samuel88/code-comprehension-check-skill -a <agente> -y --copy
```

Cosa fa questo comando, in ordine:

1. Clona il repo e trova `code-comprehension-check/SKILL.md` al suo interno.
2. Copia la skill nella directory giusta **per l'agente che indichi con `-a`** — ad esempio `-a claude-code` installa in `.claude/skills/`, `-a opencode` in `.opencode/skills/`. Se usi un client che segue lo standard senza una directory propria (o vuoi un'installazione portabile tra più client), usa `-a universal`: installa nel percorso standard `.agents/skills/`.
3. Ometti `-a` per farti chiedere interattivamente quale agente scegliere tra quelli rilevati nel progetto.
4. Crea (o aggiorna) uno **`skills-lock.json`** nella root del progetto, che traccia quali skill sono installate e da dove — è quello che permette poi a `skills update` di funzionare. Vedi la sezione sotto se il progetto ne ha già uno.

`--copy` forza una copia reale dei file invece di un symlink (comportamento di default) — più semplice da capire e da versionare per chi non ha familiarità con i symlink, consigliato soprattutto in ambito didattico.

⚠️ Rivedi sempre il contenuto di una skill prima di usarla: viene eseguita con i permessi pieni del tuo agente.

> **Nota:** se il progetto in cui installi ha un `package.json` con `devEngines.packageManager` impostato (es. forza `pnpm`), `npx` può fallire con un errore `EBADDEVENGINES` perché rispetta quel vincolo anche se stai solo scaricando uno strumento temporaneo. In quel caso usa `pnpm dlx` (o il gestore pacchetti richiesto da quel progetto) invece di `npx`.

### Se il progetto ha già uno `skills-lock.json`

Nessun problema, non c'è conflitto: ogni skill è un'entry separata nel file, quindi puoi semplicemente lanciare di nuovo `skills add` come sopra — si aggiunge accanto alle skill già tracciate senza toccarle.

C'è un caso diverso da conoscere: se hai clonato un progetto che **ha già `skills-lock.json`** ma le cartelle delle skill non ci sono (ad esempio perché non sono state committate), non serve rilanciare `add` ripetendo repo e agente per ognuna — basta ripristinarle tutte dal lockfile:

```bash
npx skills experimental_install
# oppure con pnpm:
pnpm dlx skills experimental_install
```

Legge `skills-lock.json`, riscarica ogni skill dalla fonte registrata e la reinstalla esattamente nel percorso in cui si trovava. Testato: funziona correttamente rimuovendo la cartella di una skill già tracciata e ripristinandola con questo comando.

## Aggiornamento

```bash
npx skills update
# oppure con pnpm:
pnpm dlx skills update
```

Le versioni sono taggate su Git (`vX.Y.Z`) e tracciate anche nel campo `metadata.version` del frontmatter di `SKILL.md`. Vedi `CHANGELOG.md` per la cronologia delle modifiche.

## Validazione

Prima di taggare una nuova release, verifica la conformità allo standard con il validator ufficiale:

```bash
npx skills-ref validate code-comprehension-check
```
