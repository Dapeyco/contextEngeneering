# Validation Checklist

Checklist for validating lean instruction structures.

## Root File

- [ ] Under 20 lines
- [ ] Contains project description (1 line)
- [ ] Contains reading policy (blockquote)
- [ ] Contains intent index (table with keywords)
- [ ] No section headers (`##`)
- [ ] No long content/details

## Modules

- [ ] Module directory exists (`AGENTS/` or similar)
- [ ] Files use numbered prefixes (`10-`, `20-`, etc.)
- [ ] Files use kebab-case
- [ ] Each module has `Scope:` header
- [ ] Each module has `Read when:` header
- [ ] Each module has `Skip when:` header
- [ ] Content is domain-specific

## Routing

- [ ] Keywords match user vocabulary
- [ ] Each intent maps to one module
- [ ] No auto-loading (`@file.md`)
- [ ] Plain Markdown links used

## Maintenance

- [ ] Root stays small
- [ ] New content goes to modules
- [ ] Structure reviewed quarterly

## Tool Compatibility

- [ ] Works with AGENTS.md
- [ ] CLAUDE.md synced if needed
- [ ] GitHub Copilot compatible if needed