# lean-instructions

A lightweight skill for designing AI instruction files that stay small at startup and load detailed context only when needed.

## Purpose

`lean-instructions` helps structure instruction systems such as `CLAUDE.md`, `AGENTS.md`, and `copilot-instructions.md` using a **minimal root router** plus **linked domain modules**.

The goal is simple:

- reduce startup token cost,
- avoid bloated always-loaded instruction files,
- improve routing to the right information,
- and keep instruction systems easier to maintain over time.

## Core principle

**The root instructions file is a router, not a knowledge base.**

The root file should contain only the information that must always be loaded:

- a short project description,
- a reading policy,
- and an intent index pointing to specialized modules.

Everything else should live in domain-specific files that are read on demand.

## What this skill does

This skill is designed for anyone who wants to:

- create a clean `CLAUDE.md`, `AGENTS.md`, or Copilot instruction structure,
- split a large instruction file into modular files,
- optimize context loading in AI-assisted development workflows,
- or define reusable standards for team instruction files.

It provides guidance for:

- root file design,
- module design,
- naming conventions,
- routing by intent,
- maintenance rules,
- and common mistakes to avoid.

## The pattern

The recommended structure looks like this:

```text
AGENTS.md or CLAUDE.md       ← minimal root router
AGENTS/ or CLAUDE/
  10-overview.md
  20-commands.md
  30-architecture.md
  40-deploy.md
  50-workflow.md
```

The AI should:

1. load the root file at startup,
2. identify the user intent,
3. read one relevant module first,
4. read a second module only if the task clearly depends on it.

## Why this matters

Large instruction files often become noisy, expensive, and hard to maintain.

When every session starts by loading commands, architecture, deployment, workflow notes, and project background all at once, the AI spends context on information that may be irrelevant to the current task.

A lean router-based structure improves this by keeping:

- **always-on context** minimal,
- **task-specific context** explicit,
- and **maintenance** manageable.

## Best use cases

This skill works especially well when:

- a project has a growing `CLAUDE.md` or `AGENTS.md`,
- the instruction file mixes many unrelated domains,
- deployment, architecture, commands, and workflow information are all in one file,
- a team wants a repeatable instruction structure,
- or startup context needs to stay lightweight.

## Less useful when

This pattern may be unnecessary when:

- the project is very small,
- the instruction file is already short and stable,
- there is no meaningful domain separation,
- or the AI tool in use does not benefit from linked modular instructions.

## Root file contract

A good root file should stay short and contain only:

1. **Project description** — one short line with keywords and stack.
2. **Reading policy** — tell the AI to read only the relevant module.
3. **Intent index** — keyword-to-module mapping.

Example:

```md
Project: FastAPI content pipeline with Celery, PostgreSQL, Docker, VPS deploy.

> Read ONE relevant module at a time. Load a second only when required.
> Do not pre-load all modules.

| Intent | Module |
|--------|--------|
| stack, overview, structure | [CLAUDE/10-overview.md](CLAUDE/10-overview.md) |
| pytest, docker, commands | [CLAUDE/20-commands.md](CLAUDE/20-commands.md) |
| architecture, DB, pipeline | [CLAUDE/30-architecture.md](CLAUDE/30-architecture.md) |
| deploy, VPS, logs, production | [CLAUDE/40-deploy.md](CLAUDE/40-deploy.md) |
```

## Module contract

Each module should help the AI confirm relevance immediately.

A strong module usually begins with:

- `Scope:` what the file covers,
- `Read when:` when to use it,
- `Skip when:` when not to use it.

It may then include only the non-obvious details for that domain, such as:

- key files,
- key commands,
- pitfalls,
- success criteria,
- constraints,
- or workflow notes.

## Naming rules

Use names that are easy for both humans and AI to understand.

Recommended:

- numbered prefixes for stable ordering,
- kebab-case,
- domain-oriented names.

Good examples:

- `10-overview.md`
- `20-commands.md`
- `30-architecture.md`
- `40-deploy.md`

Avoid vague names such as:

- `notes.md`
- `misc.md`
- `context.md`

## Design rules

This skill favors the following rules:

- minimal root,
- explicit routing,
- one domain per module,
- one module loaded first,
- optional second module only if needed,
- simple Markdown links,
- maintenance by splitting, not bloating.

## Common mistakes

Typical problems this skill tries to prevent:

- turning the root file into a full project document,
- storing commands and deployment details in the root,
- using vague module names,
- linking modules without intent keywords,
- loading too much context too early,
- writing large narrative modules instead of focused operational files.

## Repository integration

This skill can be stored in a shared repository of AI patterns, or published as a standalone resource.

Typical locations include:

- `skills/lean-instructions/`
- `.github/skills/lean-instructions/`
- internal agent repositories,
- team documentation repositories.

## Suggested companion files

To make the skill more useful, pair it with:

- example root files,
- example modular instruction trees,
- migration guides from monolithic instruction files,
- validation checklists,
- and comparison examples showing before/after results.

## Contribution ideas

Useful improvements include:

- more routing examples,
- templates for different ecosystems,
- validation tools,
- naming heuristics,
- and real-world case studies.

## Summary

`lean-instructions` is a practical skill for making AI instruction systems smaller, clearer, and more scalable.

It promotes a simple rule that remains effective across many tools and workflows:

> keep the root minimal, route by intent, and load detail only on demand.
