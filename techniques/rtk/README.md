# RTK (Red Tool Kit)

RTK is an intermediary layer between the user prompt and the AI model that reduces tokens used and read.

## Purpose

- Filter and preprocess user prompts
- Reduce unnecessary context loading
- Improve response accuracy by providing focused input
- Act as a context optimization layer

## Core Principles

1. **Intermediary** — sits between prompt and model
2. **Filtering** — removes noise from prompts
3. **Compression** — summarizes long contexts
4. **Selective loading** — provides only relevant context

## Use Cases

- Preprocess prompts before sending to the model
- Filter out irrelevant context
- Compress long conversations into key points
- Route prompts to specialized handlers

## Files

```
rtk/
├── README.md       # This file
└── rtk-core.md    # Core implementation
```

## Integration

RTK can be integrated into AI workflows as a middleware layer.