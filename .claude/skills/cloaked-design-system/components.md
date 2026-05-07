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

**Use.** Inline atomic identifier — categorizes a row, surfaces a state, or summarizes a delta. Four shape families share the *Label* schema: Tag (rectangle), Callout (microcopy pill), Status (dot pill), Stat (trend pill).

**Anatomy.**
```
Tag        ┌──────────┐
           │ Voicemail│   ← rectangle, 4px radius, body text
           └──────────┘

Callout    ╭─────────────────────╮
           │ You're locked down  │   ← full pill, link text
           ╰─────────────────────╯

Status     ╭──────────────╮
           │ • Active     │   ← full pill, leading dot + label
           ╰──────────────╯

Stat       ╭──────────────╮
           │ ↑ 4 Today    │   ← full pill, leading chevron + label
           ╰──────────────╯
```
- **Tag.** One slot — label only. No leading, no trailing.
- **Callout.** One slot — label only. No leading, no trailing.
- **Status.** Leading dot (state indicator) + label. No trailing.
- **Stat.** Leading chevron (trend direction) + label. No trailing.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `tag/default` | 4px radius, `--ct-bkgd-01` fill, `--ct-text-primary` label | Generic categorization (e.g. "Voicemail") |
| `tag/success` | 4px radius, `--ct-status-success-subtle` fill, `--ct-status-success-solid` label | Completed / positive completed states (e.g. "Done") |
| `tag/on` | 4px radius, `--ct-status-success-solid` fill, _TBD_ label | Live / active flag (e.g. "On") |
| `tag/alert` | 4px radius, `--ct-status-fail-solid` fill, _TBD_ label | Spam / blocked / dangerous (e.g. "Spam") |
| `callout` | Full pill, `--ct-bkgd-01` fill, link text | One-line affirmational microcopy |
| `status/card` | Full pill, `--ct-bkgd-01` fill, 4px dot, link text | Compact card-corner status (e.g. "Active") |
| `status/default` | Full pill, `--ct-bkgd-01` fill, 6px dot, body-small text | Inert status (e.g. "Next scan Oct 12") |
| `status/active` | Full pill, `--ct-divider` fill, 8px dot, body-small text | Live / scanning state (e.g. "Scan time 22:24:52") |
| `stat/up` | Full pill, `--ct-status-success-subtle` fill, ↑ chevron + value in `--ct-status-success-solid` | Positive delta on a KPI (e.g. "↑ 4 Today") |
| `stat/down` | Full pill, `--ct-status-fail-subtle` fill, ↓ chevron + value in `--ct-status-fail-solid` | Negative delta on a KPI (e.g. "↓ 4 Today") |

**Sizing.**
- **Tag.** Height `--ct-spacing-32`; padding-inline `--ct-spacing-12`; padding-block `--ct-spacing-4`; border-radius `--ct-spacing-4`.
- **Callout.** Padding-inline `--ct-spacing-16`; padding-block `--ct-spacing-12`; border-radius 100px (full pill — no token; any value ≥ height/2 collapses to a pill).
- **Status / card.** Height `--ct-spacing-32`; padding-inline `--ct-spacing-12`; padding-block `--ct-spacing-8`; border-radius `--ct-spacing-24`; gap `--ct-spacing-8`; dot 4px.
- **Status / default.** Same paddings as `/card`; border-radius 100px (full pill); gap `--ct-spacing-4`; dot 6px.
- **Status / active.** Same paddings as `/card`; border-radius `--ct-spacing-40`; gap `--ct-spacing-4`; dot 8px.
- **Stat.** Height `--ct-spacing-32`; padding-left `--ct-spacing-8`; padding-right `--ct-spacing-12`; padding-block `--ct-spacing-4`; border-radius `--ct-spacing-20`; gap `--ct-spacing-4`; chevron icon 16×16.

**Tokens.**

*Tag*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`tag/default`) | background | `--ct-bkgd-01` |
| Container (`tag/success`) | background | `--ct-status-success-subtle` |
| Container (`tag/on`) | background | `--ct-status-success-solid` |
| Container (`tag/alert`) | background | `--ct-status-fail-solid` |
| Label (`tag/default`) | color | `--ct-text-primary` |
| Label (`tag/success`) | color | `--ct-status-success-solid` |
| Label (`tag/on`) | color | _TBD_ |
| Label (`tag/alert`) | color | _TBD_ |
| Label (all) | font (apply all 5 sub-tokens) | `--ct-text-body-family`, `--ct-text-body-weight`, `--ct-text-body-size`, `--ct-text-body-line-height`, `--ct-text-body-letter-spacing` |

> _`tag/on` and `tag/alert` label colors have no fitting token in the current system. The closest visual fit, `--ct-text-ai-primary`, is restricted by SKILL.md §5.2 to AI surfaces only. Add a fixed-cream-on-status-solid token in Figma and re-export before resolving these slots._

*Callout*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Label | color | `--ct-text-primary` |
| Label | font (apply all 5 sub-tokens) | `--ct-text-link-family`, `--ct-text-link-weight`, `--ct-text-link-size`, `--ct-text-link-line-height`, `--ct-text-link-letter-spacing` |

*Status*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`/card`, `/default`) | background | `--ct-bkgd-01` |
| Container (`/active`) | background | `--ct-divider` |
| Dot | fill | `--ct-text-primary` |
| Label | color | `--ct-text-primary` |
| Label (`/card`) | font (apply all 5 sub-tokens) | `--ct-text-link-family`, `--ct-text-link-weight`, `--ct-text-link-size`, `--ct-text-link-line-height`, `--ct-text-link-letter-spacing` |
| Label (`/default`, `/active`) | font (apply all 5 sub-tokens) | `--ct-text-body-small-family`, `--ct-text-body-small-weight`, `--ct-text-body-small-size`, `--ct-text-body-small-line-height`, `--ct-text-body-small-letter-spacing` |

*Stat*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`stat/up`) | background | `--ct-status-success-subtle` |
| Container (`stat/down`) | background | `--ct-status-fail-subtle` |
| Chevron + Label (`stat/up`) | color | `--ct-status-success-solid` |
| Chevron + Label (`stat/down`) | color | `--ct-status-fail-solid` |
| Label (all) | font (apply all 5 sub-tokens) | `--ct-text-link-family`, `--ct-text-link-weight`, `--ct-text-link-size`, `--ct-text-link-line-height`, `--ct-text-link-letter-spacing` |

**Don't.**
- Don't add an icon, count, or trailing element to `tag/*`. Tag is one slot — a single label, full stop. (SKILL.md §9.3 spirit — list-row affordance rules apply.)
- Don't bold any label or counter. All weights are 400 (SKILL.md §2.5). Differentiate `success` / `on` / `alert` by color and background, never by weight.
- Don't reach for Simula on any Label variant. Tag is 16px (body), Status `/default` and `/active` are 14px (body-small), Callout / Status `/card` / Stat are 12px (link) — all sans, all outside Simula scope (SKILL.md §2.4 / §6).
- Don't apply `--ct-text-ai-primary` to a Tag (or any Label) just because the Figma master references it — §5.2 restricts fixed-dark text tokens to the AI input and the FAQ band. Wait for the missing token; do not substitute by hand.
- Don't replace the Status dot or the Stat chevron with a `chevron.right` or other navigation glyph. The leading slot is a state indicator, not an affordance (SKILL.md §9.3 spirit).
- Don't tint `tag/*` with `--ct-monitoring-*`, `--ct-guard-*`, or `--ct-identity-*`. Category tokens are reserved for feature surfaces; Tag uses status tokens only (SKILL.md §9.1).
- Don't shrink Tag / Stat below `--ct-spacing-32` height, or remove their inline padding. The 32px row keeps Label aligned with the rest of the system's inline rhythm.

**Figma.**
- Page node: `16082:15637`
- Tag masters: `16015:3815` (default), `16084:18864` (success), `16084:18884` (on), `16015:3814` (alert)
- Callout master: `16910:7736`
- Status masters: `16608:7532` (card), `16169:2623` (default), `16169:2618` (active)
- Stat masters: `17384:8700` (up), `17384:8699` (down)
- File: Playlist — Toolkit
- Link: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16082-15637

### 4. Banner

**Use.** Persistent advisory message that lives inside a list or sheet — explains a process state in plain language. Calmer than a Status row, denser than a Hero, never a transient toast.

**Anatomy.**
```
╭───────────────────────────────────────────╮
│  WHAT HAPPENS NEXT                        │   ← eyebrow (small, primary)
│                                           │
│  Cloaked has sent removal requests to     │   ← body (regular, secondary)
│  broker sites. Most sites take 7–14 days  │
│  to process.                              │
╰───────────────────────────────────────────╯
```
- Container — rounded rectangle, warm-grey fill.
- Content column — eyebrow on top, body paragraph below.
- No leading icon, no trailing affordance.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `info` | Warm-grey container, eyebrow + body paragraph stacked, 20px radius | Process explanation that needs to live on screen until resolved (e.g., "Removal in progress") |

**Sizing.**
- Container: padding `--ct-spacing-16` (all sides); border-radius `--ct-spacing-20`; horizontal gap `--ct-spacing-16` (reserved for a future multi-slot variant; inert in `info`).
- Content column: vertical gap `--ct-spacing-8` between eyebrow and body.

**Tokens.**

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-banner-container` |
| Eyebrow | color | `--ct-banner-text-primary` |
| Eyebrow | text-transform | `uppercase` |
| Eyebrow | font (apply all 5 sub-tokens) | `--ct-text-body-small-family`, `--ct-text-body-small-weight`, `--ct-text-body-small-size`, `--ct-text-body-small-line-height`, `--ct-text-body-small-letter-spacing` |
| Body | color | `--ct-banner-text-secondary` |
| Body | font (apply all 5 sub-tokens) | `--ct-text-body-family`, `--ct-text-body-weight`, `--ct-text-body-size`, `--ct-text-body-line-height`, `--ct-text-body-letter-spacing` |

> _Source the eyebrow string in natural case (`"what happens next"`); CSS handles uppercase. This mirrors SKILL.md §6.5's "CSS owns casing" principle — Banner eyebrow uses `uppercase` rather than `capitalize` because it's a kicker pattern, not a section title._

**Don't.**
- Don't bold the eyebrow or body. All weights are 400 (SKILL.md §2.5). Hierarchy comes from size + color, not weight.
- Don't reach for Simula on a Banner. Eyebrow (14px) and body (16px) are both sans, both outside Simula scope (SKILL.md §2.4 / §6).
- Don't add a trailing chevron, close X, or action button. Banner has no trailing slot — if dismissal is needed, the parent surface owns it (SKILL.md §9.3 spirit).
- Don't drop a shadow or add a border on the container. The `--ct-banner-container` fill is the separation; cards never shadow (SKILL.md §9.2).
- Don't substitute `--ct-text-primary` / `--ct-text-secondary` for Banner text. `--ct-banner-text-*` is tuned for the warm-grey container; cross-using lowers contrast.
- Don't repurpose Banner with a status fill (e.g., `--ct-status-fail-subtle`) to fake an "alert" variant. There is no alert Banner in this spec — surface the request rather than improvising (SKILL.md §2.3).
- Don't hand-type the eyebrow as `"WHAT HAPPENS NEXT"`. Source it naturally and let CSS uppercase it (see note above).

**Figma.**
- Master component node: `16061:8388`
- Page node: `16953:9417`
- File: Playlist — Toolkit
- Link: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16953-9417

### 5. Control

**Use.** Stateful interactive control — switches a state, picks one value from a small set, or moves between top-level views. Four families share the *Control* schema: Tabs (top-nav strip), Toggle (boolean), Dropdown (picker), Segment (mutually-exclusive set).

**Anatomy.**
```
Tabs        ┌────────────────────────────────────────┐
            │  Tab 1     Tab 2     Tab 3             │   ← strip; one item underlined (active)
            └────────────────────────────────────────┘   ← 1px hairline below the strip

Toggle      ╭──────────╮              ╭──────────╮
            │ ●        │              │        ● │       ← 72×32 pill, knob slides L↔R
            ╰──────────╯              ╰──────────╯
                off                       on

Dropdown    ╭──────────────╮
            │ All        ⌄ │       ← cream pill, label + chevron
            ╰──────────────╯

Segment     ╭───────╮ ╭───────╮ ╭───────╮
            │ Week  │ │ Month │ │ Year  │       ← strip; one item filled (active), others outlined
            ╰───────╯ ╰───────╯ ╰───────╯
```
- **Tabs** — strip of items, one underlined. Items have no inline padding; the strip's gap is the separation.
- **Toggle** — pill track + circular knob. Position is the affordance.
- **Dropdown** — single pill; label + trailing chevron flips on expand.
- **Segment** — strip of items, one filled. Container gap is the separation.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `tabs/active` | Body label, 1px solid `--ct-cta-primary-container` underline | Selected tab in a top-nav strip |
| `tabs/inactive` | Body label at `--ct-opacity-disabled`, no underline | Unselected tabs in same strip |
| `toggle/off` | 72×32 pill, `--ct-cta-secondary-container` track, knob nudged left | Boolean off |
| `toggle/on` | 72×32 pill, `--ct-status-success-solid` track, knob nudged right | Boolean on |
| `dropdown/collapsed` | Cream pill, body-small label + chevron-down | Picker, idle |
| `dropdown/expanded` | Cream pill, body-small label + chevron-up | Picker, open |
| `segment/active` | `--ct-cta-primary-container` fill, link label in `--ct-cta-primary-text` | Selected option in a 2–3 segment row |
| `segment/inactive` | 1px `--ct-cta-secondary-container` border, no fill, link label in `--ct-text-primary` | Unselected segments in same row |

**Sizing.**
- **Tabs item** — padding-block `--ct-spacing-20`; underline 1px solid (active only). No padding-inline.
- **Tabs strip** — padding-top `--ct-spacing-48`; padding-inline `--ct-spacing-16`; gap `--ct-spacing-24`; border-bottom 1px solid `--ct-divider`; container fill `transparent`; `backdrop-filter: blur(16px)` (no blur token in current system — to be added).
- **Toggle** — width `--ct-spacing-72`; height `--ct-spacing-32`; border-radius `--ct-spacing-16`. Knob `--ct-spacing-20` × `--ct-spacing-20`, vertically centered (6px clearance top/bottom = (32 − 20) / 2). Horizontally inset ~6px from the side the knob rests on (left when off, right when on). Knob fill is bundled in the SVG asset (currently white) — for theme-aware fill, Figma must export it as a variable.
- **Dropdown** — padding-left `--ct-spacing-16`; padding-right `--ct-spacing-12`; padding-block `--ct-spacing-8`; gap `--ct-spacing-4`; border-radius `--ct-spacing-24`; chevron 16×16; overflow-clip.
- **Segment item** — width = equal share of `(strip-width − sum-of-gaps) / count`; padding-block `--ct-spacing-12`; padding-inline `10px` (no matching `--ct-spacing-10` in current system; left as raw value until a token lands); border-radius `--ct-spacing-16`.
- **Segment strip** — gap `--ct-spacing-16`.

**Tokens.**

*Tabs*

| Slot | Property | Token |
| --- | --- | --- |
| Strip | background | `transparent` |
| Strip | backdrop-filter | `blur(16px)` (no token — pending) |
| Strip | border-bottom | `1px solid --ct-divider` |
| Item label | color | `--ct-text-primary` |
| Item label | font (apply all 5 sub-tokens) | `--ct-text-body-family`, `--ct-text-body-weight`, `--ct-text-body-size`, `--ct-text-body-line-height`, `--ct-text-body-letter-spacing` |
| Item (`tabs/active`) | border-bottom | `1px solid --ct-cta-primary-container` |
| Item (`tabs/inactive`) | opacity | `--ct-opacity-disabled` |

*Toggle*

| Slot | Property | Token |
| --- | --- | --- |
| Track (`toggle/off`) | background | `--ct-cta-secondary-container` |
| Track (`toggle/on`) | background | `--ct-status-success-solid` |
| Knob | fill | bundled in SVG asset (no token; see Sizing) |

*Dropdown*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Label | color | `--ct-text-primary` |
| Label | font (apply all 5 sub-tokens) | `--ct-text-body-small-family`, `--ct-text-body-small-weight`, `--ct-text-body-small-size`, `--ct-text-body-small-line-height`, `--ct-text-body-small-letter-spacing` |
| Chevron | color | inherits from `--ct-text-primary` |

*Segment*

| Slot | Property | Token |
| --- | --- | --- |
| Item (`segment/active`) | background | `--ct-cta-primary-container` |
| Item (`segment/active`) label | color | `--ct-cta-primary-text` |
| Item (`segment/inactive`) | border | `1px solid --ct-cta-secondary-container` |
| Item (`segment/inactive`) | background | `transparent` |
| Item (`segment/inactive`) label | color | `--ct-text-primary` |
| Item label (all) | font (apply all 5 sub-tokens) | `--ct-text-link-family`, `--ct-text-link-weight`, `--ct-text-link-size`, `--ct-text-link-line-height`, `--ct-text-link-letter-spacing` |

**Don't.**
- Don't add padding-inline to Tabs items. The strip's `--ct-spacing-24` gap is the separation; the underline is the affordance (SKILL.md §9.3 spirit).
- Don't bold any active state. Differentiate active from inactive using underline / fill / opacity, never weight (SKILL.md §2.5).
- Don't reach for Simula on any Control label. Tabs (16px), Dropdown (14px), Segment (12px) are all sans, all outside Simula scope (SKILL.md §2.4 / §6).
- Don't apply `--ct-color-*` primitives to Toggle. The ON track is `--ct-status-success-solid`, never `--ct-color-green-01` directly (SKILL.md §4.4).
- Don't substitute `--ct-bkgd-02` for the active Segment label color. The semantically-paired text token for `--ct-cta-primary-container` is `--ct-cta-primary-text`; mismatch breaks dark-theme contrast.
- Don't add a chevron-right or arrow to a Segment, Tab, or Toggle. The fill / underline / knob position is the affordance (SKILL.md §9.3 spirit).
- Don't drop a shadow on Toggle, Dropdown, or Segment containers. Surfaces never shadow (SKILL.md §9.2).
- Don't introduce a new Control family (e.g., switch, slider, checkbox). The four above are the closed set — surface the request rather than improvising (SKILL.md §7.1, §2.3).

**Figma.**
- Page node: `16022:7383`
- Tabs item: `16022:7486`
- Tabs strip: `16022:7491` (3-tap), `16022:7499` (5-tap). Master is named "Taps" in Figma — likely a typo for "Tabs".
- Toggle: `16031:7853` (on), `16031:7854` (off)
- Dropdown: `16767:13472` (collapsed), `16767:13477` (expanded)
- Segment item: `16054:8063` (active), `16960:10261` and `16960:10262` (inactive)
- Segment strip: `16960:10273`
- File: Playlist — Toolkit
- Link: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16022-7383

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
