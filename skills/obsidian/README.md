# obsidian

Hybrid human + AI project memory skill. Manages `vault/` inside the repo — plans, tasks, decisions, graphify outputs.

## Role in the ecosystem

| Skill | Scope |
|-------|-------|
| **obsidian** (this skill) | `vault/` — plans, tasks, decisions |
| lean-instructions | `AGENTS.md` + `AGENTS/` — agent instructions |
| graphify | `vault/graphify/` — codebase mapping |

## Prerequisites

- `graphify` installed (for automatic codebase mapping on `/init`)
- Obsidian plugins: **Dataview** (essential), **Kanban** (essential)

## Usage

Invoke via the `Skill` tool with `skill: "obsidian"`, then use the commands below.

## Commands

| Command | Action |
|---------|--------|
| `/init` | Initialize `./vault/` (folders, YAML templates, kanban, .aignore) |
| `/status` | Summary of active/blocked tasks and ongoing plans |
| `/kanban` | Human-readable task view + `status` field updates |
| `/query "<question>"` | Query vault + graphify for code-related questions |
| `/archive` | Move `status: done` notes to `99_archive/` |

## Quick start

```bash
# In the project directory, from Claude Code:
# 1. Invoke the skill
# 2. Type: /init
# → vault/ created with templates, kanban, plans, .aignore
# → graphify runs automatically if codebase already exists
```

## Generated vault structure

```
vault/
├── .aignore
├── plans/
│   ├── plans.md          ← Dataview index
│   └── plan-{feature}.md
├── tasks/
│   ├── kanban.md         ← Dataview view
│   └── task-{id}.md
├── decisions/
│   └── decision-{id}.md
├── graphify/             ← graphify outputs (read-only)
└── 99_archive/
```

## Important rules

- Never touch `AGENTS.md` or `AGENTS/` (lean-instructions scope)
- `vault/graphify/` is **read-only** — only `graphify` writes there
- `vault/.obsidian/` must be in the repo's `.gitignore`
- Only scan targeted YAML files, never all of `vault/`

---

# obsidian (Français)

Skill de mémoire projet hybride humain + IA. Gère `vault/` dans le repo — plans, tâches, décisions, sorties graphify.

## Rôle dans l'écosystème

| Skill | Périmètre |
|-------|-----------|
| **obsidian** (ce skill) | `vault/` — plans, tâches, décisions |
| lean-instructions | `AGENTS.md` + `AGENTS/` — instructions agent |
| graphify | `vault/graphify/` — cartographie du code |

## Prérequis

- `graphify` installé (pour la cartographie code automatique au `/init`)
- Plugins Obsidian : **Dataview** (essentiel), **Kanban** (essentiel)

## Utilisation

Invoquer via le `Skill` tool avec `skill: "obsidian"`, puis utiliser les commandes ci-dessous.

## Commandes

| Commande | Action |
|----------|--------|
| `/init` | Initialise `./vault/` (dossiers, templates YAML, kanban, .aignore) |
| `/status` | Résumé des tâches actives/bloquées et plans en cours |
| `/kanban` | Vue tâches lisible + mise à jour du champ `status` |
| `/query "<question>"` | Interroge vault + graphify si question sur le code |
| `/archive` | Déplace les notes `status: done` vers `99_archive/` |

## Démarrage rapide

```bash
# Dans le répertoire du projet, depuis Claude Code :
# 1. Invoquer le skill
# 2. Taper : /init
# → vault/ créé avec templates, kanban, plans, .aignore
# → graphify lancé automatiquement si codebase existant
```

## Structure vault générée

```
vault/
├── .aignore
├── plans/
│   ├── plans.md          ← index Dataview
│   └── plan-{feature}.md
├── tasks/
│   ├── kanban.md         ← vue Dataview
│   └── task-{id}.md
├── decisions/
│   └── decision-{id}.md
├── graphify/             ← sorties graphify (lecture seule)
└── 99_archive/
```

## Règles importantes

- Ne jamais toucher à `AGENTS.md` ni `AGENTS/` (périmètre lean-instructions)
- `vault/graphify/` est en **lecture seule** — seul `graphify` y écrit
- `vault/.obsidian/` doit être dans `.gitignore` du repo
- Ne scanner que les fichiers YAML ciblés, jamais tout `vault/`
