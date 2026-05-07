---
name: obsidian
description: Use when initializing or managing project documentation in Obsidian — creating vault structure, tracking task status, querying project memory, or coordinating with graphify for codebase mapping. Trigger when a project needs structured Markdown notes readable by both humans (Kanban, Dataview) and AI agents.
metadata:
  author: David PEYRONNE DaPeyCo
  created: "2026-05-02"
---

# Obsidian — Mémoire projet hybride humain + IA

> Ce skill gère `vault/` — plans, tâches, décisions, sorties graphify.
> `lean-instructions` gère `AGENTS.md` + `AGENTS/` — instructions de l'agent.
> `graphify` gère `vault/graphify/` — cartographie du code (lecture seule pour ce skill).

---

## Structure vault (dans le repo)

```
mon-projet/
├── AGENTS.md              ← lean-instructions (racine, inchangé)
├── AGENTS/
├── vault/                 ← ce skill
│   ├── .aignore
│   ├── plans/
│   │   ├── plans.md       ← index Dataview
│   │   └── plan-{feature}.md
│   ├── tasks/
│   │   ├── kanban.md      ← vue Dataview
│   │   └── task-{id}.md
│   ├── decisions/
│   │   └── decision-{id}.md
│   ├── graphify/          ← sorties graphify (lecture seule)
│   └── 99_archive/
└── src/
```

---

## Commandes

### /init

Initialise `./vault/` au démarrage d'un projet :

1. Crée `plans/`, `tasks/`, `decisions/`, `assets/`, `99_archive/`, `graphify/`
2. Génère les templates YAML (tâche, plan, ADR) dans chaque dossier
3. Génère `tasks/kanban.md` et `plans/plans.md` avec requêtes Dataview
4. Ajoute `vault/.obsidian/` au `.gitignore` du repo
5. Génère `vault/.aignore`
6. Lance `graphify . --obsidian --obsidian-dir ./vault` si le codebase existe déjà

Ne touche **jamais** à `AGENTS.md` ni `AGENTS/`.

### /status

Lecture rapide de l'état du projet pour l'IA :
- Lit les frontmatters YAML de `vault/tasks/` et `vault/plans/` via l'outil Read
- Retourne un résumé : tâches actives, bloquées, plans en cours

### /kanban

Affiche la vue `tasks/kanban.md`. Peut mettre à jour le champ `status` dans le frontmatter d'une tâche unitaire.

### /query "\<question\>"

Répond à une question métier en combinant :
- Lecture YAML de `vault/tasks/`, `vault/plans/`, `vault/decisions/`
- `vault/graphify/GRAPH_REPORT.md` si la question porte sur l'architecture du code

### /archive

Déplace les notes avec `status: done` vers `vault/99_archive/`.

---

## Protocole graphify ↔ vault

**Commande standard** :
```bash
graphify . --obsidian --obsidian-dir ./vault
```

**Lancer graphify si** :
- `vault/graphify/` est absent
- `vault/graphify/graph.json` est plus ancien que 7 jours
- Après un refactoring majeur (renommage de modules, restructuration de dossiers)
- Début de session sur un codebase inconnu ou non cartographié

**Sorties dans `vault/graphify/`** (lecture seule — seul graphify y écrit) :
- `GRAPH_REPORT.md` — rapport lisible humain
- `graph.json` — GraphRAG machine-readable
- `index.md` + articles par communauté — navigables dans Obsidian

---

## Conventions YAML (frontmatter)

**Tâche** (`type: task`) :
```yaml
type: task
project: NomDuProjet
status: todo           # todo | in-progress | blocked | done
priority: medium       # low | medium | high
owner: david
due: 2026-05-10
next_action: "prochaine action concrète"
blocked: false
updated: 2026-05-02
```

**Plan** (`type: plan`) :
```yaml
type: plan
project: NomDuProjet
status: active         # draft | active | completed | archived
priority: high
updated: 2026-05-02
```

**Décision ADR** (`type: decision`) :
```yaml
type: decision
project: NomDuProjet
status: accepted       # proposed | accepted | deprecated | superseded
date: 2026-05-02
```

---

## Règles de lecture IA

1. Lire `vault/.aignore` en premier — connaître les exclusions avant tout scan
2. Ne jamais scanner tout `vault/` — utiliser les requêtes YAML ou les commandes du skill
3. Ordre de priorité :
   - Instructions agent → `AGENTS.md` (lean-instructions)
   - Mémoire métier → `vault/tasks/`, `vault/plans/`, `vault/decisions/`
   - Architecture code → `vault/graphify/GRAPH_REPORT.md`
4. Ne lire `vault/99_archive/` que si explicitement demandé
5. Ne relancer graphify que si `vault/graphify/` est absent ou `graph.json` plus vieux que 7 jours

---

## Fichier `.aignore` (généré par `/init`)

```
# Config interne Obsidian
.obsidian/

# Archives (lecture sur demande uniquement)
99_archive/

# Fichiers binaires non lisibles
*.canvas
*.zip
*.db

# Médias lourds non documentaires
assets/*.mp4
assets/*.mov
```

---

## Vues Dataview (`tasks/kanban.md`)

```dataview
TABLE priority, next_action, due
FROM "tasks"
WHERE type = "task" AND status != "done"
SORT priority DESC
```

Tâches bloquées :
```dataview
LIST next_action
FROM "tasks"
WHERE blocked = true
```

Plans actifs (`plans/plans.md`) :
```dataview
TABLE status, priority, updated
FROM "plans"
WHERE type = "plan"
SORT status, priority DESC
```

---

## Plugins Obsidian recommandés

| Plugin | Rôle | Priorité |
|--------|------|----------|
| Dataview | Requêtes YAML | Essentiel |
| Kanban | Vue Kanban | Essentiel |
| Templater | Génération templates | Recommandé |
| Periodic Notes | Daily/Weekly | Optionnel |
| Full Calendar | Vue calendrier `due` | Optionnel |
