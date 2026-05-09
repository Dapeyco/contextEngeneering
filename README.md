# contextEngineering

A practical repository for designing lighter, smarter, and more maintainable AI context systems.

This project focuses on **context engineering** for AI-assisted development: reducing startup token cost, improving instruction routing, structuring reusable skills, and organizing workspace knowledge so an AI can load only what it needs when it needs it.

## Why this repository exists

Most AI workspace instruction files become too large over time. They accumulate architecture notes, command lists, deployment steps, workflow rules, and project details in a single always-loaded file.

That creates three problems:

- Higher startup token cost.
- Slower and noisier responses.
- Harder maintenance for humans and AI alike.

This repository explores a better pattern:

- a **minimal root instruction file**,
- **on-demand modules** by domain,
- **explicit routing by intent**,
- and reusable methods, tools, and experiments for context optimization.

## Repository scope

This repository is intended as a home for:

- reusable AI skills,
- context optimization patterns,
- prompt and instruction design techniques,
- workflow structures for agents and copilots,
- supporting tools and experiments such as **RTK** and **Graphify**.

The goal is not just to save tokens, but to make AI workspaces more reliable, modular, and easier to scale.

## Core idea

The main pattern promoted here is simple:

1. Keep the root instructions file minimal.
2. Treat it as a **router**, not a knowledge base.
3. Store detailed knowledge in focused modules.
4. Read modules only when the task requires them.
5. Avoid loading unrelated context at startup.

In short:

> Minimal always-on context. Rich on-demand context.

## Current contents

### Skills

- **lean-instructions** — a production-oriented skill for structuring `CLAUDE.md`, `AGENTS.md`, and `copilot-instructions.md` using a lightweight root router and linked modules.
- **obsidian** — a documentation-oriented skill for initializing and managing project knowledge in an Obsidian vault, including Markdown structure, task tracking, and AI-readable workspace memory.

### Techniques

This repository may also include methods and supporting concepts such as:

- **RTK**
- **Graphify**
- context routing patterns
- modular instruction design
- retrieval-oriented workspace structures

## Recommended repository structure

```text
contextEngineering/
├── README.md
├── skills/
│   ├── lean-instructions/
│   │   ├── SKILL.md
│   │   ├── README.md
│   │   └── examples/
│   └── obsidian/
│       ├── SKILL.md
│       └── README.md
├── techniques/
│   ├── rtk/
│   └── graphify/
├── templates/
│   ├── AGENTS.md
│   ├── CLAUDE.md
│   └── copilot-instructions.md
└── docs/
    ├── concepts/
    ├── comparisons/
    └── publishing/
```

Adjust the structure as the repository grows, but keep the separation clear between:

- **skills**: reusable operational patterns,
- **techniques**: methods and design approaches,
- **templates**: ready-to-copy files,
- **docs**: explanations, comparisons, and publishing guidance.

## Who this is for

This repository is for people who work seriously with AI in development workflows, including:

- developers using Claude Code, Codex, Copilot, Cursor, or similar tools,
- teams maintaining large workspace instruction files,
- builders designing internal AI standards,
- contributors experimenting with better context-loading strategies.

## Design principles

Everything in this repository should follow these principles:

- **Minimal by default** — always-loaded files must stay small.
- **Modular by design** — one domain, one module.
- **Explicit routing** — the AI should know where to read next.
- **Human-readable** — structure must help people too, not only models.
- **Tool-agnostic when possible** — patterns should work across multiple AI tools.
- **Production-minded** — examples should be realistic, maintainable, and reusable.

## First skill: Lean Workspace Instructions

The first skill in this repository is built around a strong rule:

**The root instructions file is a router, not a document.**

That means:

- the root file contains only the always-needed information,
- detailed instructions are moved into linked domain modules,
- and the AI reads only the relevant module for the current task.

This keeps the startup context lightweight while preserving access to operational depth when needed.

## Example use case

A traditional root file might contain stack details, deployment commands, test workflows, architecture notes, and production procedures all in one place.

With the lean pattern:

- the root file only says where each topic lives,
- a deployment request loads the deployment module,
- a feature request loads the development or architecture module,
- and unrelated knowledge stays out of the current context.

## Contributing

Contributions are welcome if they improve one or more of the following:

- context efficiency,
- instruction quality,
- modular workspace design,
- routing reliability,
- portability across AI tools.

Useful contributions include:

- new skills,
- improved templates,
- comparative examples,
- real-world case studies,
- tooling that helps generate, validate, or maintain modular instruction systems.

Before contributing, favor:

- simple structures,
- clear naming,
- short always-on files,
- examples over theory,
- and reproducible patterns.

## Roadmap ideas

Potential future additions:

- validation tools for root router quality,
- keyword coverage checks for intent indexes,
- generators for modular instruction layouts,
- migration guides from large monolithic instruction files,
- comparisons across Claude, Copilot, Codex, and other ecosystems.

## License

Choose a permissive license if you want broad reuse by the AI tooling community, such as MIT.

## Status

This repository is an evolving workspace for practical context engineering patterns.

It starts with lean instruction design, but the broader ambition is to build a useful collection of methods, templates, and tools for making AI workspaces lighter, clearer, and more effective.
