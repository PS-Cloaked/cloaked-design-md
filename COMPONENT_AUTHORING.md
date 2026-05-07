# Component Authoring Guide

> **Audience: Claude Code (with or without Figma MCP).**
> Read this file in full before writing any component `.md`.
> If Figma MCP is connected, treat Figma as the ground truth for specs (sizes, colors, tokens). If not, write specs from the user's description and flag any guesses.

---

## What you're writing

You are authoring component documentation files inside the `components/` folder of this repo (`cloaked-design-md`). Each file describes one component (or a small tightly-related group). The files are consumed by **other LLMs and humans who do not have Figma access** — so each file must be self-contained enough to recreate the component without opening Figma.

The `.md` files are **not** a Figma export. They are a rule book: when to use the component, what slots it has, what changes between variants, what's forbidden. Specs (px, hex, exact token names) are included so the file is self-contained, but the file's primary job is to teach *intent*, not to mirror Figma pixel-for-pixel.

---

## Source of truth, in order

1. **Figma** (`Foundation /` pages, accessed via MCP if connected) — the canonical visual.
2. **`tokens/*.css`** — the canonical token names and values. Never invent token names; always grep these files first.
3. **`INSTRUCTIONS.md`** — philosophy, naming rules, Kit voice, forbidden patterns. Component files must not contradict this.
4. **Existing component files** in `components/` — for tone, structure, and cross-references.
5. **The user's chat instructions** — for intent and scope.

If sources disagree: Figma wins on visual specs, `tokens/*.css` wins on token names, `INSTRUCTIONS.md` wins on rules. Surface the conflict to the user before resolving silently.

---

## Before you write — checklist

Run through this every time, before drafting:

1. **Read `INSTRUCTIONS.md`** in full. The component file's tone, vocabulary, and forbidden patterns must match.
2. **Read all four `tokens/*.css` files** (`colors.css`, `themes.css`, `numbers.css`, `typography.css`). Note the exact token names available. You will reference these by name; never approximate.
3. **Read any existing component files** in `components/`. Match their structure and section ordering. If `feature-list-item.md` or `list-item.md` already exists, use them as the structural template.
4. **If Figma MCP is available**: open the `Foundation / <Component>` page in Figma. Read every variant. Note the actual values for spacing, sizing, color tokens used.
5. **If Figma MCP is not available**: ask the user for screenshots of the Figma page, or work from their description. **Mark anything you guessed with `> TODO: confirm with Figma` so it can be fixed later.**

---

## Method (Approach C) — what goes in the file, what doesn't

Every spec in a component file falls into one of three buckets:

### Bucket 1 — Reference a token

If the value is in `tokens/*.css`, use the token name. Do not write the literal value.

✅ `color: var(--ct-text-primary)`
❌ `color: #141410`

✅ `padding: var(--ct-spacing-20) var(--ct-spacing-16)`
❌ `padding: 20px 16px`

### Bucket 2 — Inline-explain (small atoms)

Small visual atoms that aren't reused enough to deserve their own component file get explained inline, where they're used.

Examples:
- An icon used in one slot → describe inline ("24×24, monolinear, currentColor"). Don't link to an `icon.md` that doesn't exist.
- A hairline divider used inside a row → describe inline ("0.5pt, `var(--ct-divider)`, full-width inset 0").

### Bucket 3 — Link to another component file

If a real reusable component handles this slot's content, link to its `.md` file with a relative path.

✅ `The trailing badge uses [Label / Tag](./label.md).`

Only link to files that exist (or will exist as part of the same PR). Don't link to placeholder files.

---

## File structure — required sections

Every component `.md` follows this skeleton. Add sections only if the component genuinely needs them; don't pad.

````markdown
# <Component Name>

> Source of truth: Figma — `Foundation / <Component>`
> Do not hand-edit specs that disagree with Figma.

<One-paragraph description: what this component is and where it lives in the system. If the component has sibling files (e.g. `list-item.md` ↔ `feature-list-item.md`), name the sibling and the boundary between them.>

---

## 1. When to use which / Decision

<A small decision tree or table. The reader's first question is always "which variant do I use?" — answer it before describing anything.>

---

## 2. <Variant A>

**Anatomy** — ASCII sketch or labelled diagram if it helps.

**Layout** — container width, padding, alignment. Use spacing tokens.

**Slots** — what content goes where. Cite typography + color tokens for each.

**Background** — what surface token, or "inherits from parent".

**Composition** — how multiple instances stack, separator behavior, what surrounds it.

**Don't** — 2–4 specific anti-patterns.

---

## 3. <Variant B> …

---

## N. Theme behavior

<Token-to-theme mapping table. Confirm both `data-theme="light"` and `data-theme="dark"` render correctly. Reference the semantic tokens used; do not write hex.>
````

Skip section 1 if the component has only one variant. Skip the theme section if the component has no theme-sensitive surface (rare).

---

## Voice and length

- **English only.** All `.md` content is English, even when the user writes to you in Korean.
- **Short, declarative sentences.** Match the existing files (`INSTRUCTIONS.md`, `feature-list-item.md`).
- **Imperative `Do` / `Don't` lists** when stating rules. No softening ("you might want to consider…").
- **No filler.** No "In summary," no "It's worth noting that," no marketing tone.
- **Keep each variant section under ~80 lines.** If you're going longer, you're probably writing reference material that belongs in Figma.
- **Never bold for hierarchy in body prose.** Use headings and section breaks. (Bold inside `Do` / `Don't` bullets is fine for the action verb.)

---

## Forbidden in component files

These mirror `INSTRUCTIONS.md` — but apply specifically to the writing of `.md` files:

- ❌ **Don't paraphrase `INSTRUCTIONS.md`.** Reference it by name when relevant ("see `INSTRUCTIONS.md` — Forbidden patterns").
- ❌ **Don't invent token names.** Every `--ct-*` you write must exist in `tokens/*.css`. If you need one that doesn't exist, stop and ask the user.
- ❌ **Don't write hex values inline.** Always go through tokens. Only exception: documenting that a primitive token *equals* a hex (and that belongs in `tokens.md`, not a component file).
- ❌ **Don't write "etc." or "and so on."** List exhaustively or don't list at all.
- ❌ **Don't add example code in framework-specific syntax** (React JSX, SwiftUI, Tailwind class strings) unless the user explicitly asks. Components are framework-agnostic. Use generic CSS or plain prose.
- ❌ **Don't include marketing-style headers** ("Beautiful, accessible list items"). The reader wants rules, not pitch.

---

## Working with the user

The user is the design owner. They prefer:

- **Korean conversation, English code/`.md`.**
- **Plan first, then execute.** For any non-trivial change, propose the structure (section list, slot list, decisions to make) and wait for approval before drafting.
- **Mechanical replacements can run unattended.** Renaming `--old-token` to `--new-token` across files doesn't need a plan. Anything involving judgment does.
- **Diff-by-diff review.** When editing existing files, show changes incrementally. Don't rewrite a whole file when a section needs adjusting.
- **No formatting changes outside the requested edit.** Don't reflow paragraphs, don't reorder sections, don't "fix" things that weren't asked about.

When uncertain, **ask** rather than guess. The cost of a clarifying question is far below the cost of a wrong-by-design component file that gets propagated to other files.

---

## Quality bar — before handing back

Before saying "done," check:

1. ✅ Every `--ct-*` token referenced exists in `tokens/*.css` (grep to confirm).
2. ✅ No raw hex codes outside fenced `.css` example blocks demonstrating a token's *value*.
3. ✅ No `9:41`, no fake status bar, no chevron.right on list rows, no drop shadows — none of the forbidden patterns from `INSTRUCTIONS.md`.
4. ✅ Both `data-theme="light"` and `data-theme="dark"` are addressed, or the file explicitly states the component is fixed-theme (rare).
5. ✅ Cross-references to other component files use relative paths and only point to files that exist.
6. ✅ `Don't` lists are specific and concrete, not vague ("don't make it look bad").
7. ✅ The file is < ~250 lines for a single-variant component, < ~500 for a multi-variant. If longer, you're probably embedding reference material.

---

## Workflow — typical session

```
1. User: "Let's write components/<name>.md"
2. You: Read INSTRUCTIONS.md, tokens/*.css, any existing components/*.md.
        Read Figma `Foundation / <Component>` page (via MCP, if available).
3. You: Propose a plan — section list, slots identified, decisions needed.
4. User: Approves or edits the plan.
5. You: Draft the file. Show it to the user.
6. User: Reviews, comments.
7. You: Edit incrementally — only touch what was flagged.
8. User: Approves and commits / pushes (or asks you to stage).
```

The user runs `git status`, `git add`, `git commit`, `git push` themselves unless they explicitly delegate.

---

## When this guide is wrong

This guide describes the convention as of its writing. If the user gives an instruction that contradicts something here, **the user's instruction wins for that session** — and ask them whether to update this guide too. The guide should evolve with the system.
