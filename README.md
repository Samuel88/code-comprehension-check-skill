# code-comprehension-check

Agent Skill conforme allo standard [agentskills.io](https://agentskills.io/specification): interroga uno studente su una codebase reale con domande mirate a file/funzioni/logica effettivamente presenti, non un quiz teorico. Vedi `SKILL.md` per le istruzioni complete.

## Installazione

Copia (o `git submodule add`) questa cartella dentro `.agents/skills/code-comprehension-check` nel progetto in cui vuoi usarla:

```bash
git submodule add <url-di-questo-repo> .agents/skills/code-comprehension-check
```

oppure, senza submodule:

```bash
git clone <url-di-questo-repo> /tmp/ccc && cp -r /tmp/ccc/* /percorso/progetto/.agents/skills/code-comprehension-check/
```

## Aggiornamento

- Con submodule: `git submodule update --remote .agents/skills/code-comprehension-check`
- Senza submodule: ripeti la copia dall'ultima versione taggata

Le versioni sono taggate su Git (`vX.Y.Z`) e tracciate anche nel campo `metadata.version` del frontmatter di `SKILL.md`. Vedi `CHANGELOG.md` per la cronologia delle modifiche.

## Validazione

Prima di taggare una nuova release, verifica la conformità allo standard:

```bash
skills-ref validate .
```
