# Graphify

Graphify creates a knowledge graph of project files, clustered by communities, outputting HTML + JSON + audit reports.

## Purpose

- Visualize project file relationships
- Cluster files by domain/directory
- Generate HTML visualization
- Generate JSON for programmatic use
- Produce audit reports

## Core Features

1. **File mapping** — scan and catalog all project files
2. **Clustering** — group files by communities (directories, imports)
3. **Graph generation** — create node/link graph
4. **Output formats** — HTML, JSON, audit reports

## Use Cases

- Understand project structure at a glance
- Find related files quickly
- Avoid re-reading entire project to understand hierarchy
- Generate documentation

## Files

```
graphify/
├── README.md       # This file
└── graphify-core.md
```

## Trigger

Use `/graphify` command to invoke.