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

**Use.** Covers all list rows and stat/empty placeholders within a single component family. Anatomy splits into two classes: Standard row (with Avatar) / Nested (without Avatar).

**Anatomy — Class A (Standard row).**
[Avatar 40×40]  [Title           ]  [Trailing?]
[Meta             ]
[─────── Divider (bottom, optional) ─────────]

- Container: `--ct-spacing-20` padding all sides, `--ct-bkgd-02`, width 393px
- Avatar: 40×40 leading slot (see Avatar slot section below)
- Title: `var(--ct-text-body-*)` + `--ct-text-primary`, single-line ellipsis
- Meta: `var(--ct-text-body-small-*)` + `--ct-text-secondary`, single-line ellipsis
- Trailing: optional, variant-dependent (see Trailing slot section below)
- Divider: 1px line at bottom, `--ct-divider`. The row owns its own divider — do not draw it externally.

**Anatomy — Class B (Nested).**

Used when the row sits inside a parent container (e.g. a Card or Section) that already provides horizontal padding. Does not span screen edge-to-edge.

| Subtype | Anatomy |
|---|---|
| Stat | Label (w-210) + Value (right-aligned, primary). Width 322px, py-16, no horizontal padding, no background. Lives inside a parent container. |
| Empty | 360×240 placeholder block. Single message, absolute-centered. Not a row — represents the empty state of the entire list region. |

**Title content rule (page-dependent).**

The same List Item component, but the Title's starting content depends on which page it appears on.

| Page | Title starts with | Example |
|---|---|---|
| Activities | **Action verb** (what happened) | "Spam call blocked" |
| Detail | **Entity name** (who/where) | "(322) 142-8932" |

Activities answers *what happened*. Detail answers *who/where*. Meta fills in the missing half — phone number on Activities, scam type on Detail.

**Avatar slot — 7 types.** Determined by data availability and contact type.

| Type | When | Visual |
|---|---|---|
| `Avatar_default` | System action / feature row | Icon shell + sub-icon (e.g. `Default_monitoring/Darkweb`, `Default_guard/call`, `Default_Identity/Authenticator`) |
| `Avatar_default` (Card shape) | Identity card variant | 40px wrapper containing a 22×34 rounded card |
| `Avatar_Flags` | VPN | Country flag icon |
| `Avatar_Category` | Password | Colored circle base + key icon overlay |
| `Avatar_Brand logo` | Brand entity (image=true) | Third-party logo (Lululemon, Spokeo, etc.) |
| `Avatar_CloakedPay_Brand Logo` | Card with brand | 40px wrapper + 22×34 brand-filled card |
| `Avatar_caller initicial` | Person contact, no photo | 40px circle + uppercase initial in white (`--ct-cta-primary-text`) |
| `Avatar_Custom Image` | Person contact, has photo | 40px filled with user-uploaded photo |

**Image boolean toggle.** Many variants carry an `image: boolean` prop.

| image | System contact | Brand contact | Person contact |
|---|---|---|---|
| `false` | `Avatar_default` (icon) | `Avatar_default` (icon) | `Avatar_caller initicial` (initial letter) |
| `true` | (n/a) | `Avatar_Brand logo` | `Avatar_Custom Image` (photo) |

→ Meaning: "show real avatar instead of fallback"

**Trailing slot — 5 types + none.**

| Type | Visual | When |
|---|---|---|
| Plain text | Content-driven width (82px ~ 172px), right-aligned, `var(--ct-text-body-*)` + `--ct-text-primary` | VPN duration, phone numbers, status counts |
| Label badge | Cream pill: `--ct-bkgd-01`, h-32, padding `--ct-spacing-12`/`--ct-spacing-4`, radius 4px | Block Spam type ("SMS"/"Call"/"Email") |
| 2-line text block | Title primary + Subtitle secondary, right-aligned, fixed width | VPN: "2h 14m" / "1.2GB" |
| Icon (24×24) | Type icon | Inbox row type indicator, Password copy icon |
| (none) | Slot omitted entirely | Activity/Monitor Dark Web, Data Removal (info goes in body inline) |

**Body inline content.** Content placed inside the body slot rather than in a separate trailing slot.

| Pattern | When | Anatomy |
|---|---|---|
| Inline number/status | Data Removal, Monitoring | Title row splits left/right: left=source, right=number/status |
| Progress bar | Data Removal (Not started, In Progress) | Title row + progress bar (h-8, full-width, fill `--ct-brand`, track `--ct-bkgd-01`) + Meta |

**Variants by context.**

| Context | Notable variants | Notes |
|---|---|---|
| Activities | Create Identity, Monitor Dark Web, Use VPN, Block Spam, Monitor Data Removal | **Title = action verb** ("Spam call blocked"). Activity log. |
| Detail | (Same component as Activity, different page) | **Title = entity name** ("(322) 142-8932"). Entity detail. |
| Monitoring Data | Dark web monitoring, Data Removal | Same component as Activity; only meta text differs. |
| Guard | SMS Guard, Call Guard, Email Guard, VPN | Trailing = Label badge (Spam types) or 2-line text (VPN). |
| Identity | Phone, Email, Card, Password, Account | Each carries `image: boolean` toggle (except Password). |
| Identity/Inbox | Call, Voicemail, Missed call, Message, Email | Single base + type prop. Trailing icon paired 1:1 with type. |
| Stat | Stat (no Avatar) | Class B — nested subtype. |
| Empty | empty-state | Class B — placeholder block. |

**Inbox type ↔ trailing icon mapping.**

| Type | Trailing icon |
|---|---|
| Call | `informational/call` |
| Voicemail | `informational/voicemail` |
| Missed call | `informational/missed` |
| Message | `feature/identity/sms` |
| Email | `feature/identity/email` |

**Layout patterns — 2 types.**

| Pattern | Body | Trailing | When |
|---|---|---|---|
| Default (gap-based) | flex-1 | auto | Most Activity rows, Identity (general). |
| Fixed-width (justify-between) | fixed width | fixed width | VPN (any page), Identity/Inbox throughout. |

→ Layout signal: use fixed-width when body or trailing contains multi-line / long content.

**Sizing.**
- Row width: 393px (Class A standard)
- Stat width: 322px (Class B nested — parent provides horizontal padding)
- Empty: 360×240
- Inner padding: `--ct-spacing-20` (Class A) / `--ct-spacing-16` vertical only (Stat)
- Avatar: 40×40 (`--ct-spacing-40`)
- Avatar ↔ Body gap: `--ct-spacing-12`
- Body ↔ Trailing gap: `--ct-spacing-8` (default), or fixed-width split
- Title ↔ Meta gap: `--ct-spacing-8`

**Tokens.**
- Background: `--ct-bkgd-02`
- Title: `var(--ct-text-body-*)` + `--ct-text-primary`
- Meta: `var(--ct-text-body-small-*)` + `--ct-text-secondary`
- Divider: `--ct-divider`
- Avatar initial color: `--ct-cta-primary-text` (white)
- Label badge bg: `--ct-bkgd-01`
- Progress bar fill: `--ct-brand`
- Progress bar track: `--ct-bkgd-01`
- Title/Meta overflow: single-line ellipsis

**Don't.**
- ❌ Do not add chevron right (SKILL.md §9.3) — the row itself is the affordance.
- ❌ Do not mix Avatar types arbitrarily — they are determined by `image` boolean and contact type (System/Brand/Person).
- ❌ Do not enforce Cloaked color rules on Brand logos — brand fidelity wins.
- ❌ Do not allow Title or Meta to wrap to multiple lines — enforce single-line ellipsis.
- ❌ Do not place Stat at the screen edge — it must sit nested inside a parent's horizontal padding.
- ❌ Do not treat Empty like a "row" — it is the empty placeholder for the entire list region.
- ❌ Do not start an Activities title with an entity name — start with an action verb ("Spam call blocked", not "(322) 142-8932").
- ❌ Do not start a Detail title with an action verb — start with the entity name.

**Figma.** 6 pages — Activity / Monitoring Data / Guard / Identity / Identity-Inbox / Global (Stat-Empty).

### 7. Section Header

**Use.** First row of a section inside a list — names what's below and, when needed, exposes a single right-aligned affordance (filter or action). Sits flush on the section's white surface; not a page title, not a card header.

**Anatomy.**
```
default     ┌─────────────────────────────────────────────────┐
            │  Scan history                                   │   ← title only, capitalized
            └─────────────────────────────────────────────────┘

dropdown    ┌─────────────────────────────────────────────────┐
            │  Scan history                       ╭ All  ⌄ ╮  │   ← title + Dropdown chip
            │                                     ╰────────╯  │
            └─────────────────────────────────────────────────┘

action      ┌─────────────────────────────────────────────────┐
            │  Scan history                              Edit │   ← title + plain-text action
            └─────────────────────────────────────────────────┘
```
- One row, two slots: a leading title (flex 1) and a variant-specific trailing slot.
- No leading icon, no chevron, no divider — the row sits on the same `--ct-bkgd-02` surface as the rows beneath it.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `default` | Title only, no trailing slot | Section name with no affordance (most common) |
| `dropdown` | Title + Dropdown chip ([Component 5 — Control / `dropdown/collapsed`](#5-control)) on the right | Section is filterable (e.g. "Scan history" filtered by "All / Phone / Email") |
| `action` | Title + plain-text label (e.g. "Edit") on the right, body size, primary color, no container | Section has a single text affordance — bulk action, edit, manage |

**Sizing.**
- Container: width 393px; padding-top `--ct-spacing-40`; padding-bottom `--ct-spacing-12`; padding-inline `--ct-spacing-16`; gap `--ct-spacing-12` between title and trailing (inert on `default`); `align-items: center`.
- Title: `flex: 1`; height `--ct-spacing-32`; single-line.
- Trailing (`dropdown`): full Dropdown chip — see [Component 5 — Control](#5-control) Sizing for chip dimensions (32px height, radius `--ct-spacing-24`, cream pill, 16×16 chevron).
- Trailing (`action`): intrinsic body-text height; no container, no padding.

**Tokens.**

*Container*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | padding-top | `--ct-spacing-40` |
| Container | padding-bottom | `--ct-spacing-12` |
| Container | padding-inline | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-12` |

*Title (all variants)*

| Slot | Property | Token |
| --- | --- | --- |
| Title | color | `--ct-text-primary` |
| Title | text-transform | `capitalize` |
| Title | font (apply all 5 sub-tokens) | `--ct-text-h3-family`, `--ct-text-h3-weight`, `--ct-text-h3-size`, `--ct-text-h3-line-height`, `--ct-text-h3-letter-spacing` |

> _Source the title string in natural case (`"scan history"`); CSS handles the capitalization (SKILL.md §6.5). Figma renders the title at line-height 1 / letter-spacing 0.1px, while `--ct-text-h3-*` is line-height 1.15 / letter-spacing -0.003em — known token-export drift; reference the H3 token as the only 20px sans token, and resolve the drift in Figma._

*Trailing (`dropdown`)* — see [Component 5 — Control](#5-control) Tokens / Dropdown.

*Trailing (`action`)*

| Slot | Property | Token |
| --- | --- | --- |
| Action label | color | `--ct-text-primary` |
| Action label | font (apply all 5 sub-tokens) | `--ct-text-body-family`, `--ct-text-body-weight`, `--ct-text-body-size`, `--ct-text-body-line-height`, `--ct-text-body-letter-spacing` |

**Don't.**
- Don't add a leading icon, avatar, or chevron to the title slot. Section Header has one leading slot — title only (SKILL.md §9.3 spirit).
- Don't add a `chevron.right` or arrow after the title or trailing. The section below is the affordance; the header is not a navigation row (SKILL.md §9.3).
- Don't reach for Simula on the title. Title is 20px H3 — sans, outside Simula scope (SKILL.md §2.4 / §6).
- Don't bold the title or action label to differentiate variants. Variants differ by **trailing slot**, never by weight (SKILL.md §2.5).
- Don't hand-type the title in Title Case (`"Scan History"`) or upper case (`"SCAN HISTORY"`). Source naturally and let CSS `capitalize` do the work (SKILL.md §6.5).
- Don't put an icon in the `action` trailing slot. Action is text-only — if a chevron is needed, the variant is `dropdown`, not `action`.
- Don't introduce a fourth variant (e.g., `action+icon`, `link`, `more`). The three above are the closed set; surface the request rather than improvising (SKILL.md §7.1, §2.3).
- Don't draw a hairline (`--ct-divider`) above or below the header. The row sits on the same `--ct-bkgd-02` surface as the section beneath it; separation comes from the cream gap above the section, not from a line on the header (SKILL.md §9.2).
- Don't substitute `--ct-bkgd-01` for the container background. The header shares the white sheet with the rows it labels — a cream container would re-introduce the band-style separation the system avoids.

**Figma.**
- Master component node: `16206:3359`
- Variants: `17492:13415` (default), `17826:13427` (dropdown — chip `17826:13429`), `17826:13433` (action — label `17826:13450`)
- File: Playlist — Toolkit
- Link: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16206-3359

### 8. Timeline
_TBD_

### 9. Footer
_TBD_

### 10. Navigation
_TBD_

### 11. Card / Feature
_TBD_

### 12. Card / Dashboard
_TBD_

### 13. Hero / Feature
_TBD_

### 14. Hero / Kit Briefing
_TBD_

### 15. Hero / Notification
_TBD_

---
