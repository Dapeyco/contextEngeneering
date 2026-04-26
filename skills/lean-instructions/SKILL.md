---
name: lean-instructions
description: Use when structuring or reviewing AI workspace instructions (AGENTS.md, CLAUDE.md, copilot-instructions.md) — minimizes startup token cost via a root router plus on-demand modules.
metadata:
  author: David PEYRONNE DaPeyCo
  created: "2026-04-26"
---

# Lean Workspace Instructions

## Overview

The root instructions file is a **router**, not a knowledge base.

Keep the root minimal and always-on; move task-specific details to linked modules. Modules are read on demand — nothing should be loaded at startup except the router.

## Canonical Structure

Use `AGENTS.md` + `AGENTS/` as the canonical layout. It is the most portable format across tools.

```text
AGENTS.md (router)          ← loaded at every session startup — keep under 20 lines
AGENTS/
  10-overview.md            ← read on demand when needed
  20-commands.md
  30-architecture.md
  40-vps-production.md
  50-workflow.md
```

**For tools that only read `CLAUDE.md`** (e.g. older Claude Code versions), add a copy:
```bash
cp AGENTS.md CLAUDE.md
```

**Naming:** use numbered prefixes for ordering, kebab-case, domain-oriented file names.

Good: `30-architecture.md`, `40-vps-production.md`
Bad: `notes.md`, `misc.md`, `context.md`

## Compatibility

| File | Tool |
|------|------|
| `AGENTS.md` | OpenAI Codex, multi-agent, Claude Code |
| `CLAUDE.md` | Claude Code (copy of AGENTS.md if needed) |
| `.github/copilot-instructions.md` | GitHub Copilot |
| `*.instructions.md` | Scoped instructions in editors and agent tools |

Exact loading behavior depends on the host tool.

## Safety — Before Any Modification

Before touching any existing instructions file:

**Option A — commit backup (preferred in a Git repo):**
```bash
git add AGENTS.md && git commit -m "chore: backup instructions before restructure"
```

**Option B — create a backup file:**
```bash
cp AGENTS.md AGENTS.md.bak
```

Do not modify the file until one of these two actions has been completed.

## Root File Contract

The root file should contain only the always-needed elements below:

**1. One-line project description**
Include the project keywords and stack.

**2. Reading policy**
Tell the AI how to load modules:

```md
> Read ONE module at a time. Load a second only when the first clearly depends on it or the task explicitly spans two domains.
> Do not pre-load all modules at startup.
```

**3. Intent index**
One line per domain: keywords → link.

```md
> Read the relevant module. Load ONE at a time. Do not pre-load all.

| Intent | Module |
|--------|--------|
| stack, objective, structure | [AGENTS/10-overview.md](AGENTS/10-overview.md) |
| pytest, ruff, alembic, celery, docker | [AGENTS/20-commands.md](AGENTS/20-commands.md) |
| connectors, DB, Celery, architecture | [AGENTS/30-architecture.md](AGENTS/30-architecture.md) |
| SSH, VPS, deploy, logs, production | [AGENTS/40-vps-production.md](AGENTS/40-vps-production.md) |
| specs, plans, workflow | [AGENTS/50-workflow.md](AGENTS/50-workflow.md) |
```

**Keywords must match real user vocabulary** — they are the routing triggers.

## Module Contract

Every module should open with a header block so the AI can confirm relevance before reading further:

```md
# Architecture

Scope: connectors, BaseConnector, ContentItem, data flow, DB, Celery, publishers, services, tests.
Read when: adding a connector, modifying the pipeline, or touching DB/Celery/publishers.
Skip when: the task is purely about deployment, commands, or project overview.

## Key files
- connectors/base/connector.py
- db/repositories/

## Key commands
- alembic upgrade head
- pytest src/aggregator/tests/

## Pitfalls
- Never import telegram_publisher at module level (circular import).

## Done when
- New connector passes unit tests.
- collect() returns `(article, is_new)` correctly.
```

Sections are optional. Include only what is non-obvious for that domain.

## Routing Examples

| User request | Load first | Load second if needed |
|-------------|------------|----------------------|
| "publish to prod / deploy" | `40-vps-production.md` | — |
| "add a DB migration" | `40-database.md` or the commands module | — |
| "understand the codebase" | `10-overview.md` | `30-architecture.md` if a deeper dive is needed |
| "fix a bug in the connector" | `30-architecture.md` | — |
| "run the tests" | `20-commands.md` | — |
| "add a feature + deploy it" | `30-architecture.md` | `40-vps-production.md` |

## What NEVER Goes in the Root

- `##` section headers, if they encourage the root to become a document instead of a router.
- Command lists, architecture details, VPS details, or any other deep content.
- More than one table or more than one blockquote.

If you find yourself adding content, it belongs in a module.

## Red Flags — Stop, You're Going Wrong

| Thought | Problem |
|---------|---------|
| "Let me add details here so it's clearer." | The root is a router, not a document. Move the content to a module. |
| "I'll use `@file.md` so it loads automatically." | That defeats lazy loading. Use plain Markdown links. |
| "I'll add section headers to organize the root." | The root should stay flat and compact. |
| "The content is good; the structure can wait." | Without routing, the AI may load too much or too little. Structure comes first. |
| "One big module is fine for now." | Split by domain. One scope, one module. |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| `@AGENTS/file.md` in the root | Use plain Markdown links instead of auto-loading references. |
| Plain links with no keywords | Add intent keywords: `pytest, docker → [link]`. |
| No reading policy | Add the `Read ONE module at a time` blockquote. |
| Module without a Scope header | Add `Scope:` and `Read when:` at the top of every module. |
| Root over the target size | Move content into a module. |
| Root turned into a full document | Remove detail and keep only routing. |

## Maintenance Rule

If the root grows beyond the target size, split a module instead of compressing the root.

## Fallback Policy

If no intent matches clearly:
1. Start with `10-overview.md`.
2. If the task still lacks context, ask a short clarifying question.
3. Only load additional modules when the task clearly requires them.

## Versioning Note

This pattern is intentionally simple:
- minimal root,
- explicit routing,
- task-specific modules,
- incremental loading,
- small maintenance cost.

That is what keeps startup overhead low while still making the workspace useful.
