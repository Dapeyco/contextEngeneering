# Example: FastAPI Project

Example of a lean instruction structure for a FastAPI project.

## Before (Monolithic)

```md
# Project

FastAPI content pipeline with Celery, PostgreSQL.

## Stack
- FastAPI
- Celery
- PostgreSQL

## Commands
- pytest
- alembic upgrade head
- docker-compose up

## Architecture
- connectors/base/connector.py
- db/repositories/
- ...

( ... 200+ lines later ... )
```

## After (Lean Router)

### AGENTS.md (Router)

```md
# FastAPI Content Pipeline

> Read ONE module at a time. Load second only when required.

| Intent | Module |
|--------|--------|
| stack, overview, structure | [AGENTS/10-overview.md](AGENTS/10-overview.md) |
| pytest, alembic, docker, commands | [AGENTS/20-commands.md](AGENTS/20-commands.md) |
| architecture, DB, pipeline | [AGENTS/30-architecture.md](AGENTS/30-architecture.md) |
| deploy, production | [AGENTS/40-deploy.md](AGENTS/40-deploy.md) |
```

### AGENTS/10-overview.md

```md
# Overview

Scope: project purpose, stack, structure.
Read when: understanding project at a glance.
Skip when: task is about specific domain.

- FastAPI REST API
- Celery for async tasks
- PostgreSQL for persistence
```

### AGENTS/20-commands.md

```md
# Commands

Scope: pytest, alembic, docker commands.
Read when: running tests or migrations.
Skip when: architecture or deployment task.

- pytest src/
- alembic upgrade head
- docker-compose up -d
```

### AGENTS/30-architecture.md

```md
# Architecture

Scope: connectors, DB, pipeline, services.
Read when: modifying pipeline or adding features.
Skip when: commands or deployment task.

- connectors/base/connector.py
- db/repositories/
- services/
```

### AGENTS/40-deploy.md

```md
# Deployment

Scope: VPS, SSH, production, logs.
Read when: deploying to production.
Skip when: development or commands task.

- SSH to VPS
- docker-compose pull
- tail -f logs/app.log
```

## Result

| Metric | Before | After |
|--------|--------|-------|
| Startup lines | ~200 | 15 |
| Modules loaded | all | 1-2 |