# Graphify Core

## Core Features

### File Scanner

Scans project directory and catalogs all files.

### Clustering Algorithm

Groups files by:
- Directory structure
- Import relationships
- File extension patterns
- Naming conventions

### Graph Output

Generates node/link graph structure.

### Output Formats

- **HTML** — interactive visualization
- **JSON** — programmatic use
- **Audit report** — file statistics

## Example Output

```json
{
  "nodes": [
    {"id": "src/main.py", "label": "main.py", "type": "file"},
    {"id": "src/utils.py", "label": "utils.py", "type": "file"}
  ],
  "links": [
    {"source": "src/main.py", "target": "src/utils.py", "type": "import"}
  ],
  "clusters": [
    {"name": "src", "files": ["main.py", "utils.py"]}
  ]
}
```

## Usage

```bash
graphify /path/to/project --output html
graphify /path/to/project --output json
graphify /path/to/project --output audit
```