# code-comprehension-check

Agent Skill conforme allo standard [agentskills.io](https://agentskills.io/specification): interroga uno studente su una codebase reale con domande mirate a file/funzioni/logica effettivamente presenti, non un quiz teorico. Vedi [`code-comprehension-check/SKILL.md`](code-comprehension-check/SKILL.md) per le istruzioni complete.

## Installazione

```bash
npx skills add Samuel88/code-comprehension-check-skill -a claude-code -y
# oppure con pnpm:
pnpm dlx skills add Samuel88/code-comprehension-check-skill -a claude-code -y
```

Sostituisci `claude-code` con l'agente che usi (es. `opencode`), oppure ometti `-a` per scegliere interattivamente. Il comando rileva da solo la directory giusta per l'agente scelto e crea uno `skills-lock.json` per tracciare la versione installata.

⚠️ Rivedi sempre il contenuto di una skill prima di usarla: viene eseguita con i permessi pieni del tuo agente.

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
