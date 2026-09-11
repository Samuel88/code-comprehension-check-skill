# code-comprehension-check

Agent Skill conforme allo standard [agentskills.io](https://agentskills.io/specification): interroga uno studente su una codebase reale con domande mirate a file/funzioni/logica effettivamente presenti, non un quiz teorico. Vedi `SKILL.md` per le istruzioni complete.

## Installazione

### 0. Prerequisito: dove il tuo agente cerca le skill

Lo standard [agentskills.io](https://agentskills.io/specification) definisce il *formato* di una skill, non dove i client la cercano — ogni client ha una sua directory di default (vedi [Client Showcase](https://agentskills.io/clients) per l'elenco completo). Alcuni esempi:

| Client | Directory di default |
|---|---|
| VS Code / GitHub Copilot, molti altri client conformi allo standard | `.agents/skills/` |
| Claude Code | `.claude/skills/` (locale al progetto) o `~/.claude/skills/` (personale, tutti i progetti) |

Se il tuo client non trova la skill dopo l'installazione, per prima cosa controlla la sua directory di default nella documentazione del client.

### 1. Installazione rapida via agente

Se il tuo client AI ha accesso a shell/file system, il modo più semplice è incollargli questo prompt e lasciare che faccia tutto da solo:

```
Installa la Agent Skill "code-comprehension-check" dal repository
https://github.com/Samuel88/code-comprehension-check-skill (tag v1.0.0):
determina quale directory delle skill usi tu come agente in questo progetto
(es. .agents/skills/ o .claude/skills/), clona/scarica lì dentro una
sottocartella "code-comprehension-check" contenente SKILL.md e la cartella
references/ dal repo indicato, poi conferma che la skill compare nel tuo
elenco di skill disponibili.
```

Il prompt punta deliberatamente al tag `v1.0.0` (non a `main`) per un'installazione riproducibile, copia solo `SKILL.md` e `references/` (non `README.md`/`CHANGELOG.md`, che sono metadati del repo e non fanno parte della skill secondo la spec), e lascia che sia l'agente a determinare la propria directory di default invece di fissarla tu — varia da client a client (vedi punto 0).

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

- Con submodule: `git submodule update --remote .agents/skills/code-comprehension-check`
- Senza submodule: ripeti la copia dall'ultima versione taggata

Le versioni sono taggate su Git (`vX.Y.Z`) e tracciate anche nel campo `metadata.version` del frontmatter di `SKILL.md`. Vedi `CHANGELOG.md` per la cronologia delle modifiche.

## Validazione

Prima di taggare una nuova release, verifica la conformità allo standard:

```bash
skills-ref validate .
```
