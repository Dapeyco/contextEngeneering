# Migration Guide

How to migrate from a monolithic instruction file to a lean router structure.

## Step 1: Backup

```bash
git add AGENTS.md && git commit -m "chore: backup before migration"
```

Or:

```bash
cp AGENTS.md AGENTS.md.bak
```

## Step 2: Analyze

Identify domains in the current file:

- commands / pytest / docker
- architecture / DB / services
- deployment / production
- workflow / specs

## Step 3: Create Modules

Create `AGENTS/` directory with modules:

```bash
mkdir AGENTS
touch AGENTS/10-overview.md
touch AGENTS/20-commands.md
touch AGENTS/30-architecture.md
touch AGENTS/40-deploy.md
```

## Step 4: Extract Content

Move content to appropriate modules:

- commands → `20-commands.md`
- architecture → `30-architecture.md`
- deployment → `40-deploy.md`

## Step 5: Create Router

Write minimal root:

```md
# Project Name

> Read ONE module at a time. Load second when required.

| Intent | Module |
|--------|--------|
| stack, overview | [AGENTS/10-overview.md](AGENTS/10-overview.md) |
| commands, pytest | [AGENTS/20-commands.md](AGENTS/20-commands.md) |
| architecture, DB | [AGENTS/30-architecture.md](AGENTS/30-architecture.md) |
| deploy, production | [AGENTS/40-deploy.md](AGENTS/40-deploy.md) |
```

## Step 6: Test

Test with typical requests:

- "run the tests"
- "add a feature"
- "deploy to production"

Ensure correct modules load.

## Step 7: Iterate

Refine keywords and module content based on testing.