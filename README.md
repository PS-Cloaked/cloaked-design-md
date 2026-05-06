# Cloaked Design System — .md Package

## What is this

An LLM-friendly context package for the Cloaked Design System. It bundles design tokens (`.css`), font files, and component specs (`.md`) so AI tools can understand and follow the Cloaked design language when generating code or making design decisions.

## Files

```
cloaked-design-md/
├── README.md            # This file
├── INSTRUCTIONS.md      # LLM behavior rules
├── tokens.md            # Token usage guide
├── assets.md            # Logo, icon, and asset guidelines
├── components.md        # Component specs and patterns
├── examples.md          # End-to-end usage examples
├── tokens/
│   ├── colors.css       # Color primitives (16 tokens)
│   ├── themes.css       # Light/Dark semantic tokens
│   ├── numbers.css      # Spacing + opacity tokens
│   └── typography.css   # Text styles + @font-face declarations
└── fonts/
    ├── Simula-Book.otf
    └── Simula-Italic.otf
```

## How to use with LLMs

### Quick start (Claude)

- Attach the entire repo folder to a Claude Project.
- Claude automatically picks up `INSTRUCTIONS.md` as its behavior rules.
- The remaining files are referenced as context when relevant.

### Other LLMs

- **ChatGPT** — Upload as files (subject to context limits).
- **Cursor** — Place in workspace; reference via `@`-mention.
- **API integrations** — Pass relevant files as system context.

### Example prompts

```
Create a CTA button using Cloaked design tokens.
```

```
Build a card component with the dark theme.
```

```
Style this header with --ct-text-h1.
```

## Sync with Figma

When Figma Variables or Text Styles change, export the relevant collection as JSON to the `_temp/` folder (gitignored), then regenerate the corresponding `tokens/*.css` file. Do not hand-edit token values — always regenerate from the Figma export so the CSS stays a faithful mirror of the source of truth.
