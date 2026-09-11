# code-comprehension-check

Agent Skill conforme allo standard [agentskills.io](https://agentskills.io/specification): interroga uno studente su una codebase reale con domande mirate a file/funzioni/logica effettivamente presenti, non un quiz teorico. Vedi `SKILL.md` per le istruzioni complete.

## Installazione

### 0. Prerequisito: dove il tuo agente cerca le skill

Lo standard [agentskills.io](https://agentskills.io/specification) definisce il *formato* di una skill, non dove i client la cercano — ogni client ha una sua directory di default (vedi [Client Showcase](https://agentskills.io/clients) per l'elenco completo). Alcuni esempi:

| Client | Directory di default |
|---|---|
| VS Code / GitHub Copilot, molti altri client conformi allo standard | `.agents/skills/` |
| Claude Code | `.claude/skills/` (locale al progetto) o `~/.claude/skills/` (personale, tutti i progetti) |
| OpenCode | `.opencode/skills/` (progetto) o `~/.config/opencode/skills/` (globale) — legge anche `.agents/skills/` e `.claude/skills/` senza bisogno di copie extra |
| Mistral AI Vibe | `.vibe/skills/` (progetto) o `~/.vibe/skills/` (globale) — legge anche `.agents/skills/` direttamente |

Se il tuo client non trova la skill dopo l'installazione, per prima cosa controlla la sua directory di default nella documentazione del client.

### 1. Installazione più rapida: `skills` CLI

Se hai Node.js (npm, pnpm, ecc.) installato, il modo più rapido in assoluto è il [CLI `skills`](https://github.com/vercel-labs/skills) — un package manager per Agent Skills che usa GitHub come registry e rileva da solo la directory giusta per l'agente che indichi:

```bash
npx skills add Samuel88/code-comprehension-check-skill -a claude-code -y
# equivalente con pnpm:
pnpm dlx skills add Samuel88/code-comprehension-check-skill -a claude-code -y
```

Sostituisci `claude-code` con l'agente che usi (es. `opencode`), oppure ometti `-a` per una selezione interattiva tra i client rilevati. Testato con entrambi i comandi: clonano il repo, installano la skill nella directory corretta per l'agente scelto (es. `.claude/skills/code-comprehension-check/`) e creano un `skills-lock.json` nella root del progetto per tracciare la versione installata.

⚠️ Il tool stesso lo ricorda a fine installazione: rivedi sempre il contenuto di una skill prima di usarla, perché viene eseguita con i permessi pieni del tuo agente.

### 2. In alternativa: comandi manuali

Il repo è pubblico su GitHub: https://github.com/Samuel88/code-comprehension-check-skill

Con submodule (Git, versione tracciata e aggiornabile):

```bash
git submodule add https://github.com/Samuel88/code-comprehension-check-skill.git <directory-skill-del-client>/code-comprehension-check
```

Senza submodule (copia semplice, ultima release taggata):

```bash
git clone --branch v1.0.0 https://github.com/Samuel88/code-comprehension-check-skill.git /tmp/ccc
cp -r /tmp/ccc/* <directory-skill-del-client>/code-comprehension-check/
```

Sostituisci `<directory-skill-del-client>` con quella del punto 0 (es. `.agents/skills` oppure `.claude/skills`).

### 3. Verifica che sia stata caricata

Il meccanismo varia per client, ma in generale: riavvia/ricarica la sessione dell'agente (le skill vengono scoperte all'avvio) e controlla l'elenco delle skill disponibili — in VS Code/Copilot digita `/skills` in chat, in Claude Code la skill compare nell'elenco `<system-reminder>` delle skill disponibili o puoi chiedere direttamente "quali skill hai a disposizione?".

## Aggiornamento

Le versioni sono taggate su Git (`vX.Y.Z`) e tracciate anche nel campo `metadata.version` del frontmatter di `SKILL.md`. Vedi `CHANGELOG.md` per la cronologia delle modifiche.

### 1. Aggiornamento più rapido: `skills` CLI

Se hai installato con il CLI `skills` (punto 1 dell'installazione), aggiornare è un solo comando, da eseguire nella cartella del progetto dove hai fatto l'installazione:

```bash
npx skills update
# equivalente con pnpm:
pnpm dlx skills update
```

Legge da solo `skills-lock.json` e riallinea tutte le skill installate all'ultima versione disponibile sul repository sorgente — nessun parametro da passare. Testato con entrambi i comandi.

### 2. Aggiornamento rapido via agente

Stesso principio: incolla questo prompt e lascia che l'agente confronti la versione installata con l'ultima disponibile e la sostituisca se serve.

```
Aggiorna la Agent Skill "code-comprehension-check" installata in questo
progetto all'ultima versione taggata del repository
https://github.com/Samuel88/code-comprehension-check-skill: trova la
directory in cui è installata (es. .agents/skills/code-comprehension-check
o .claude/skills/code-comprehension-check), leggi il campo
metadata.version nel suo SKILL.md, confrontalo con l'ultimo tag del
repository remoto, e se è più vecchio sostituisci SKILL.md e la cartella
references/ con quelli dell'ultimo tag. Poi dimmi da quale versione a
quale hai aggiornato.
```

### 3. In alternativa: comandi manuali

- Con submodule: `git submodule update --remote <directory-skill-del-client>/code-comprehension-check`
- Senza submodule: ripeti la copia dall'ultima versione taggata (vedi comando `git clone --branch` sopra, sostituendo il tag con quello nuovo)

## Validazione

Prima di taggare una nuova release, verifica la conformità allo standard:

```bash
skills-ref validate .
```
