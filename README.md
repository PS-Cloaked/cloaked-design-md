# Cloaked Toolkit — `.md` Package

A lightweight context bundle that teaches AI tools (Claude, Cursor, Claude Code) how to use the Cloaked design language. It contains the token CSS files, the Simula font, and a single AI-facing rules document — enough for an LLM to generate code or specs that match the system without guessing.

This package is **not** a component library. It is a rule book + token export. You drop it into your AI tool's context, and the AI follows it.

---

## Quick start

### Claude (chat / Project)

1. Attach this folder (or upload as a zip) to a Claude Project.
2. Claude picks up `cloaked-design-system/SKILL.md` automatically as its rules.
3. Ask: *"Build a CTA card using Cloaked tokens, dark theme."*

### Cursor

1. Place this folder anywhere in your workspace.
2. Reference it in chat with `@cloaked-design-md` (or `@cloaked-design-system/SKILL.md` for just the rules file).
3. Cursor reads the tokens and rules together.

### Claude Code

1. `cd` into a project that includes (or imports) this folder.
2. Open Claude Code and start working — it reads the package as repo context automatically.

### Other LLMs / API

Pass `cloaked-design-system/SKILL.md` plus the four `cloaked-design-system/tokens/*.css` files as system context. Skip the fonts unless you need to render previews.

---

## Folder structure

```
cloaked-design-md/
├── README.md                     # This file (humans)
└── cloaked-design-system/        # The skill (deployable unit)
    ├── SKILL.md                  # AI rules (read by LLMs)
    ├── components.md             # Component specs — currently TBD
    ├── examples.md               # BAD / GOOD usage — currently TBD
    ├── tokens/
    │   ├── colors.css            # 16 color primitives
    │   ├── numbers.css           # Spacing scale + opacity
    │   ├── themes.css            # Light + Dark semantic tokens
    │   └── typography.css        # Text styles + @font-face
    └── fonts/
        ├── Simula-Book.otf
        └── Simula-Italic.otf
```

---

## How tokens work

- **`cloaked-design-system/tokens/*.css` is the source of truth** for the AI. Token names and values come from there, not from prose docs.
- All token names are prefixed `--ct-*` (Cloaked Toolkit).
- Components consume **semantic** tokens (`--ct-bkgd-02`, `--ct-text-primary`, `--ct-cta-primary-container`). Color primitives (`--ct-color-*`) are backstage and should not be referenced directly.
- Themes activate via `data-theme="light"` or `data-theme="dark"` on the root element. There is no fallback.

The full rule set, including what's forbidden and how the AI should behave when something is ambiguous, lives in `cloaked-design-system/SKILL.md`.

---

## Updating tokens

Token CSS is generated from Figma Variables, **not hand-edited**. To update:

1. In Figma, open the relevant Variables collection (Colors / Numbers / Theme) or Text Styles.
2. Export to W3C DTCG JSON.
3. Regenerate the corresponding `cloaked-design-system/tokens/*.css` from the export.
4. Commit the regenerated CSS.

Hand-edits to `cloaked-design-system/tokens/*.css` will be overwritten on the next export. If a value needs to change, change it in Figma first.

---

## License

Simula is a licensed typeface. The `.otf` files in `cloaked-design-system/fonts/` are bundled for use within Cloaked products only. Do not redistribute the fonts as part of forks or external projects.
