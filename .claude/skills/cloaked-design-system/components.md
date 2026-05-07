# Cloaked Components

> Component rulebook. Every Cloaked UI follows these rules.
> Each component is defined as Use / Anatomy / Variants / Sizing / Tokens / Don't / Figma.
> Specify only what differs from the default visual properties.
>
> This file is part of SKILL.md's Required Reading.

---

## Default visual properties

Unless otherwise stated, every component inherits the defaults below. Each component spec lists only the properties that differ.
All tokens flip automatically with `data-theme` (light / dark).

---

## Component schema

Each component uses the sections below. Omit a section when the component matches the default.

- **Use.** One line — when to reach for this component.
- **Anatomy.** Slot structure (leading / title / trailing, etc.).
- **Variants.** Table form (variant / visual / when).
- **Sizing.** Only when it differs from the default.
- **Tokens.** Only when they differ from the default.
- **Don't.** Anti-patterns.
- **Figma.** Node ID or link.

---

## Components

### 1. Button
_TBD_

### 2. Divider

**Use.** Section break inside a list — labels a group of rows (e.g., a date band like "Today" above rows from that day). Not a hairline; not a generic separator.

**Anatomy.**
```
┌─────────────────────────────────────────────────┐
│  Today                                          │   ← cream band, full width
└─────────────────────────────────────────────────┘
```
- One slot: a leading label (`Label`), left-aligned, vertically centered.
- No trailing slot. No icon. The band is the affordance.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `default` | Cream band, single label, full width | Grouping list rows by section / date / category |

**Sizing.**
- Container height resolves to 28px from the formula below (do not hardcode 28px):
  - `padding-block: var(--ct-spacing-8)` (top + bottom = 16px)
  - Label intrinsic height: 12px (from `--ct-text-link-size`)
  - Total: 8 + 12 + 8 = 28px
- Container width: 100% of parent (stretches across the list).

**Tokens.**

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Container | padding-inline | `--ct-spacing-20` |
| Container | padding-block | `--ct-spacing-8` |
| Label | color | `--ct-text-primary` |
| Label | font (apply all 5 sub-tokens) | `--ct-text-link-family`, `--ct-text-link-weight`, `--ct-text-link-size`, `--ct-text-link-line-height`, `--ct-text-link-letter-spacing` |

**Don't.**
- Don't pair with a hairline (`--ct-divider`) above or below the band — the cream band is the separation; adding a hairline doubles the visual weight.
- Don't use Simula for the label. Label size (12px) is outside Simula scope; per SKILL.md §2.4 / §6, Simula is reserved for page titles and FAQ headlines.
- Don't bold the label or any other text in the slot. All weights are 400 (SKILL.md §2.5).
- Don't replace the label with an icon, kebab menu, or chevron. The right side stays empty (SKILL.md §9.3 spirit — list-row affordance rules apply here too).
- Don't shrink the band below 28px or remove the vertical padding. The rhythm of the list depends on it.

**Figma.**
- Master component node: `15978:2923`
- File: Playlist — Toolkit
- Link: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=15978-2923

### 3. Label
_TBD_

### 4. Banner
_TBD_

### 5. Control
_TBD_

### 6. List Item
_TBD_

### 7. Feature List Item
_TBD_

### 8. Section Header
_TBD_

### 9. Timeline
_TBD_

### 10. Footer
_TBD_

### 11. Navigation
_TBD_

### 12. Card / Feature
_TBD_

### 13. Card / Dashboard
_TBD_

### 14. Hero / Feature
_TBD_

### 15. Hero / Kit Briefing
_TBD_

### 16. Hero / Notification
_TBD_

---
