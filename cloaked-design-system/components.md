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

> **Font shorthand.** When the Tokens table shows `font (apply all 5) | --ct-text-<style>-*`, apply **all five** sub-tokens of that style: `-family`, `-weight`, `-size`, `-line-height`, `-letter-spacing`. Never cherry-pick. (See SKILL.md §4.2.)

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

> **Universal don'ts (apply to every component below — do not restate per-component).** SKILL.md §2 and §9 govern: no Simula on body / labels / numbers / captions (§2.4, §6); all weights are 400 (§2.5); no category tokens (`--ct-monitoring-*`, `--ct-guard-*`, `--ct-identity-*`) on neutral chrome (§9.1); no `--ct-text-ai-*` outside the AI input or FAQ band (§5.2); no shadows or borders for separation — separation is the `--ct-spacing-12` cream gap (§9.2); no `chevron.right` on rows or trailing slots (§9.3); no simulated iOS chrome `9:41` / signal / wifi / battery (§9.4); no `"Loading…"` labels — replace with status row + progress bar + state copy (§9.6); no closest-token approximation when a value lacks a matching token — surface the request and wait (§2.1); no `--ct-color-*` primitives in component fills — consume semantic tokens (§4.4); no closed-set extension — surface the request, new variants go into Figma first and re-export (§7.1, §2.3); no arbitrary opacity for disabled states — `--ct-opacity-disabled` (= 0.3) is the only sanctioned token (§4.3). Each component's **Don't.** block lists only component-specific anti-patterns.

### 1. Button

**Use.** A discrete action atom — the user taps it to commit, dismiss, navigate, or expand. Four shape families share the *Button* schema: Text (filled / outlined / pill / link) and Icon (filled / outlined). Pick the family by the action's weight, not the layout.

**Anatomy.**
```
text/primary       ╭───────────────────────────────╮
                   │          Disconnect           │   ← black-filled bar, white label
                   ╰───────────────────────────────╯

text/secondary     ┌───────────────────────────────┐
                   │     + Create new number       │   ← 1px outline, no fill
                   └───────────────────────────────┘

text/tertiary      ╭──────────────╮
                   │ Explore tools│   ← translucent pill, primary label
                   ╰──────────────╯

text/link            See Details   ← naked link, 12px, primary text

icon-primary       ╭────╮          ╭──╮
                   │ ⤢  │          │⤢ │   ← black-filled rounded square
                   ╰────╯          ╰──╯      large (48-ish) and small (24)

icon-secondary     ╭────╮          ╭──╮
                   │ →  │          │ →│   ← 1px outline circle / square
                   ╰────╯          ╰──╯      large (48) and small (24)

icon-tertiary      ╭────╮          ╭──╮
                   │ ?  │          │ ?│   ← translucent fill, no outline
                   ╰────╯          ╰──╯      large (48) and small (24)
```
- **Text/primary, text/secondary.** One slot — label only, centered. Full-width sheet CTA.
- **Text/tertiary.** One slot — label only. Intrinsic width pill, lives inline.
- **Text/link.** One slot — label only. No container.
- **Icon-primary, icon-secondary, icon-tertiary.** One slot — icon only. No label.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `text/primary` | Filled `--ct-cta-primary-container`, white label, 16px radius, 56px tall, full-width | The single most important CTA on a sheet (e.g., "Disconnect") |
| `text/secondary` | 1px solid `--ct-cta-secondary-container` outline, no fill, primary text label, 16px radius, 56px tall, full-width | Secondary CTA paired with `text/primary` (e.g., "+ Create new number") |
| `text/tertiary` | Translucent `--ct-cta-secondary-container` pill, primary text label, 100px radius, intrinsic width | Compact inline action with no full-width pressure (e.g., "Explore tools") |
| `text/link` | No container, no fill, link text (12px) in `--ct-text-primary` | Inline "see details"-style affordance, text only |
| `icon-primary/default` | Filled `--ct-cta-primary-container`, 24×24 icon, 12px padding, 24px radius | Primary icon-only action at standard density |
| `icon-primary/small` | Filled `--ct-cta-primary-container`, 16×16 icon, 4px padding, 12px radius | Primary icon-only action in dense layouts |
| `icon-secondary/large` | 48×48 circular outline, 24×24 icon centered | Secondary icon action — e.g., expand / next |
| `icon-secondary/small` | 24×24 outline, 16×16 icon, 4px padding | Compact secondary icon in dense layouts |
| `icon-tertiary/default` | Filled `--ct-cta-secondary-container`, 24×24 icon, 12px padding, 24px radius (no outline) | Header navigation actions (back, help, close) and any compact icon-only action where outlined would compete with adjacent icons that already enclose themselves (e.g. a `?` glyph that draws its own ring). The icon-pair to `text/tertiary`. |
| `icon-tertiary/small` | Filled `--ct-cta-secondary-container`, 16×16 icon, 4px padding, 12px radius (no outline) | Compact tertiary icon in dense layouts |

**Sizing.**
- **`text/primary`.** Height 56px; width 100% of parent (full-width sheet CTA); padding `--ct-spacing-16`; border-radius `--ct-spacing-16`.
- **`text/secondary`.** Height 56px; width 100% of parent; padding `10px` (no matching `--ct-spacing-*` token — write raw px); border `1px solid`; border-radius `--ct-spacing-16`.
- **`text/tertiary`.** Padding-inline `--ct-spacing-24`; padding-block `--ct-spacing-12`; border-radius 100px (full pill — no token; any value ≥ height/2 collapses to a pill).
- **`text/link`.** No container, no padding, no border. Hit area is the label's intrinsic box.
- **`icon-primary/default`.** Padding `--ct-spacing-12`; border-radius `--ct-spacing-24`; icon 24×24.
- **`icon-primary/small`.** Padding `--ct-spacing-4`; border-radius `--ct-spacing-12`; icon 16×16.
- **`icon-secondary/large`.** Total size `--ct-spacing-48` × `--ct-spacing-48`; padding `--ct-spacing-12`; icon 24×24; circular outline (full radius).
- **`icon-secondary/small`.** Total size `--ct-spacing-24` × `--ct-spacing-24`; padding `--ct-spacing-4`; icon 16×16.
- **`icon-tertiary/default`.** Total size `--ct-spacing-48` × `--ct-spacing-48`; padding `--ct-spacing-12`; icon 24×24; border-radius `--ct-spacing-24`; no outline (the fill is the container).
- **`icon-tertiary/small`.** Total size `--ct-spacing-24` × `--ct-spacing-24`; padding `--ct-spacing-4`; icon 16×16; border-radius `--ct-spacing-12`; no outline.

**Tokens.**

*Text variants*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`text/primary`) | background | `--ct-cta-primary-container` |
| Container (`text/secondary`) | border-color | `--ct-cta-secondary-container` |
| Container (`text/tertiary`) | background | `--ct-cta-secondary-container` |
| Container (`text/link`) | background | none |
| Label (`text/primary`) | color | `--ct-cta-primary-text` |
| Label (`text/secondary`) | color | `--ct-cta-secondary-text` |
| Label (`text/tertiary`, `text/link`) | color | `--ct-text-primary` |
| Label (`text/primary`, `text/secondary`, `text/tertiary`) | font (apply all 5) | `--ct-text-body-*` |
| Label (`text/link`) | font (apply all 5) | `--ct-text-link-*` |

*Icon variants*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`icon-primary/*`) | background | `--ct-cta-primary-container` |
| Container (`icon-secondary/*`) | border / outline | _TBD_ (bundled in SVG asset — see note below) |
| Container (`icon-tertiary/*`) | background | `--ct-cta-secondary-container` |
| Icon (`icon-primary/*`) | stroke | _TBD_ (bundled in SVG asset; visually `--ct-cta-primary-text`) |
| Icon (`icon-secondary/*`) | stroke | _TBD_ (bundled in SVG asset; visually `--ct-text-primary`) |
| Icon (`icon-tertiary/*`) | stroke | _TBD_ (bundled in SVG asset; visually `--ct-text-primary`) |

> _The `icon-secondary` outline and the icon strokes for both icon families are currently embedded in the SVG asset, not exported as Figma variables. This mirrors the Toggle knob caveat in §5 Control — for theme-aware fills, Figma must export them as variables and re-export. Until then, the rendered colors are visually consistent with `--ct-cta-secondary-container` (outline) and `--ct-cta-primary-text` / `--ct-text-primary` (icon strokes), but components must not hard-code those tokens against the asset._

**Don't.**
- Don't substitute `--ct-bkgd-*` or `--ct-status-*` for a button fill to fake a "muted" or "destructive" variant. There are four text variants and two icon variants in this spec — surface the request rather than improvising (SKILL.md §2.3).
- Don't replace the `icon-secondary` arrow with a `chevron.right` and drop the button at the end of a list row. The list itself is the affordance there; a trailing chevron-on-row is forbidden (SKILL.md §9.3).
- Don't shrink `text/primary` or `text/secondary` below 56px height or remove their inline padding. The 56px bar is the full-width sheet rhythm — clipping it breaks the relationship with surrounding rows.
- Don't repurpose `text/link` as a body-inline anchor inside a paragraph. It's a discrete button atom (12px, primary text, no underline), not an `<a>` inside prose.
- Don't pair `icon-primary` with a sibling text label outside the button. If the action needs words, choose `text/primary` instead — icon-primary is icon-only by design.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16053-7930) · Page `16053:7930` · Variant masters: text/primary `16031:7864`, text/secondary `16031:7866`, text/tertiary `16196:2699`, text/link `16960:10527`, icon-primary/default `16935:9348`, icon-primary/small `16960:10477`, icon-secondary/large `16054:8098`, icon-secondary/small `16078:12091`, icon-tertiary/default _TBD_ (proposed addition, not yet exported from Figma), icon-tertiary/small _TBD_

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
| Label | font (apply all 5) | `--ct-text-link-*` |

**Don't.**
- Don't pair with a hairline (`--ct-divider`) above or below the band — the cream band is the separation; adding a hairline doubles the visual weight.
- Don't replace the label with an icon, kebab menu, or chevron. The right side stays empty (SKILL.md §9.3 spirit — list-row affordance rules apply here too).
- Don't shrink the band below 28px or remove the vertical padding. The rhythm of the list depends on it.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=15978-2923) · Master component `15978:2923`

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
| Label (all) | font (apply all 5) | `--ct-text-body-*` |

> _`tag/on` and `tag/alert` label colors have no fitting token in the current system. The closest visual fit, `--ct-text-ai-primary`, is restricted by SKILL.md §5.2 to AI surfaces only. Add a fixed-cream-on-status-solid token in Figma and re-export before resolving these slots._

*Callout*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Label | color | `--ct-text-primary` |
| Label | font (apply all 5) | `--ct-text-link-*` |

*Status*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`/card`, `/default`) | background | `--ct-bkgd-01` |
| Container (`/active`) | background | `--ct-divider` |
| Dot | fill | `--ct-text-primary` |
| Label | color | `--ct-text-primary` |
| Label (`/card`) | font (apply all 5) | `--ct-text-link-*` |
| Label (`/default`, `/active`) | font (apply all 5) | `--ct-text-body-small-*` |

*Stat*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`stat/up`) | background | `--ct-status-success-subtle` |
| Container (`stat/down`) | background | `--ct-status-fail-subtle` |
| Chevron + Label (`stat/up`) | color | `--ct-status-success-solid` |
| Chevron + Label (`stat/down`) | color | `--ct-status-fail-solid` |
| Label (all) | font (apply all 5) | `--ct-text-link-*` |

**Don't.**
- Don't add an icon, count, or trailing element to `tag/*`. Tag is one slot — a single label, full stop. (SKILL.md §9.3 spirit — list-row affordance rules apply.)
- Don't replace the Status dot or the Stat chevron with a `chevron.right` or other navigation glyph. The leading slot is a state indicator, not an affordance (SKILL.md §9.3 spirit).
- Don't shrink Tag / Stat below `--ct-spacing-32` height, or remove their inline padding. The 32px row keeps Label aligned with the rest of the system's inline rhythm.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16082-15637) · Page `16082:15637` · Variant masters: tag/default `16015:3815`, tag/success `16084:18864`, tag/on `16084:18884`, tag/alert `16015:3814`, callout `16910:7736`, status/card `16608:7532`, status/default `16169:2623`, status/active `16169:2618`, stat/up `17384:8700`, stat/down `17384:8699`

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
| Eyebrow | font (apply all 5) | `--ct-text-body-small-*` |
| Body | color | `--ct-banner-text-secondary` |
| Body | font (apply all 5) | `--ct-text-body-*` |

> _Source the eyebrow string in natural case (`"what happens next"`); CSS handles uppercase. This mirrors SKILL.md §6.5's "CSS owns casing" principle — Banner eyebrow uses `uppercase` rather than `capitalize` because it's a kicker pattern, not a section title._

**Don't.**
- Don't add a trailing chevron, close X, or action button. Banner has no trailing slot — if dismissal is needed, the parent surface owns it (SKILL.md §9.3 spirit).
- Don't substitute `--ct-text-primary` / `--ct-text-secondary` for Banner text. `--ct-banner-text-*` is tuned for the warm-grey container; cross-using lowers contrast.
- Don't repurpose Banner with a status fill (e.g., `--ct-status-fail-subtle`) to fake an "alert" variant. There is no alert Banner in this spec — surface the request rather than improvising (SKILL.md §2.3).
- Don't hand-type the eyebrow as `"WHAT HAPPENS NEXT"`. Source it naturally and let CSS uppercase it (see note above).

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16953-9417) · Page `16953:9417` · Variant masters: info `16061:8388`

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
| Item label | font (apply all 5) | `--ct-text-body-*` |
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
| Label | font (apply all 5) | `--ct-text-body-small-*` |
| Chevron | color | inherits from `--ct-text-primary` |

*Segment*

| Slot | Property | Token |
| --- | --- | --- |
| Item (`segment/active`) | background | `--ct-cta-primary-container` |
| Item (`segment/active`) label | color | `--ct-cta-primary-text` |
| Item (`segment/inactive`) | border | `1px solid --ct-cta-secondary-container` |
| Item (`segment/inactive`) | background | `transparent` |
| Item (`segment/inactive`) label | color | `--ct-text-primary` |
| Item label (all) | font (apply all 5) | `--ct-text-link-*` |

**Don't.**
- Don't add padding-inline to Tabs items. The strip's `--ct-spacing-24` gap is the separation; the underline is the affordance (SKILL.md §9.3 spirit).
- Don't substitute `--ct-bkgd-02` for the active Segment label color. The semantically-paired text token for `--ct-cta-primary-container` is `--ct-cta-primary-text`; mismatch breaks dark-theme contrast.
- Don't add a chevron-right or arrow to a Segment, Tab, or Toggle. The fill / underline / knob position is the affordance (SKILL.md §9.3 spirit).

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16022-7383) · Page `16022:7383` · Variant masters: tabs/item `16022:7486`, tabs/strip-3-tap `16022:7491`, tabs/strip-5-tap `16022:7499` (master named "Taps" in Figma — likely typo for "Tabs"), toggle/on `16031:7853`, toggle/off `16031:7854`, dropdown/collapsed `16767:13472`, dropdown/expanded `16767:13477`, segment/item-active `16054:8063`, segment/item-inactive `16960:10261` and `16960:10262`, segment/strip `16960:10273`

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
- Divider: 0.5pt `--ct-divider` at row bottom. Row owns its own divider — never drawn externally.
  - **Tappable → full-bleed** (Mode A, default). Hairline reaches container edges. Put horizontal padding on the row, not the parent.
  - **Read-only → inset** (Mode B). Hairline inset by `--ct-spacing-20`. See *Composition — modes × containers*.

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
- Title ↔ Meta gap: `0` (flush — meta sits directly below title with no gap; line-height alone provides separation. No `--ct-spacing-*` token matches; written as raw `0`.)

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

**Composition — modes × containers.**

Two orthogonal axes describe how rows aggregate into a list and which surface that list sits on. Pick one mode and one container; any of the four combinations is valid.

*Axis 1 — Mode (divider behavior).* The only difference between modes is whether the row's bottom 0.5pt hairline reaches the container's left and right edges.

| Mode | Divider | Use when |
|---|---|---|
| **A — Full-bleed** *(default)* | 0.5pt `--ct-divider`, runs edge-to-edge of the container, no horizontal inset | Rows are tappable (push to detail, copy a value, play a voicemail), and dense enough to read as a continuous feed (settings, accounts, OTP codes, activity). The hairline reaching the surface edge does the visual work of "item, item, item." |
| **B — Inset** | 0.5pt `--ct-divider`, inset from the container's edges by the row's horizontal padding (typically `--ct-spacing-20`) | Rows are read-only / informational — a key/value sheet ("Your Info"), a summed total ("Total this month"), a dashboard summary ("Weekly removal"). Each row reads as a labelled fact, not an action. |

Mode B is **global** — not bound to dark surfaces. It works on cream, white, cards, hero bands, anywhere rows are facts rather than actions.

*Axis 2 — Container (surface).* Distinguished by the surface's margin from the screen edge.

| Container | Anatomy | Use when |
|---|---|---|
| **Page section** | Spans full screen width — zero left/right margin from screen edges. Optional section title above. Multiple page sections stack with a `--ct-spacing-12` cream gap that exposes `--ct-bkgd-01` (SKILL.md Pattern 5/Layering 2.1.1). | The list is the page's primary content (One-time passcodes), or it's one of several stacked sections that all read as part of the same flow (Inbox, Settings, Activity feed). Page sections feel like consecutive printed pages — chapters of one running document, not discrete objects. |
| **Card** | Explicit `--ct-spacing-16` margin from screen edges + 20px corner radius (raw — no `--ct-radius-*` token). Sits *on* the cream page like a physical card laid on a table, with cream visible around it. | The surface is a discrete object you might rearrange, dismiss, or place next to other cards (a dashboard tile, a "Your Info" panel, a "Digital health" widget). The card stands alone — a self-contained read or interaction, often with its own hero number or visual. |

**Don't.**
- ❌ Do not mix Avatar types arbitrarily — they are determined by `image` boolean and contact type (System/Brand/Person).
- ❌ Do not enforce Cloaked color rules on Brand logos — brand fidelity wins.
- ❌ Do not allow Title or Meta to wrap to multiple lines — enforce single-line ellipsis.
- ❌ Do not place Stat at the screen edge — it must sit nested inside a parent's horizontal padding.
- ❌ Do not treat Empty like a "row" — it is the empty placeholder for the entire list region.
- ❌ Do not start an Activities title with an entity name — start with an action verb ("Spam call blocked", not "(322) 142-8932").
- ❌ Do not start a Detail title with an action verb — start with the entity name.
- ❌ Do not call a surface a "card" if it has zero left/right margin from the screen edge — that's a page section, even with rounded corners. Cards must have visible cream around them.
- ❌ Do not separate stacked page sections with a divider or shadow — separation is the `--ct-spacing-12` cream gap (SKILL.md Pattern 5/Layering 2.1.1).
- ❌ Do not mix Mode A and Mode B inside one list — one container, one mode.

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
| Title | font (apply all 5) | `--ct-text-h3-*` |

> _Source the title string in natural case (`"scan history"`); CSS handles the capitalization (SKILL.md §6.5). Figma renders the title at line-height 1 / letter-spacing 0.1px, while `--ct-text-h3-*` is line-height 1.15 / letter-spacing -0.003em — known token-export drift; reference the H3 token as the only 20px sans token, and resolve the drift in Figma._

*Trailing (`dropdown`)* — see [Component 5 — Control](#5-control) Tokens / Dropdown.

*Trailing (`action`)*

| Slot | Property | Token |
| --- | --- | --- |
| Action label | color | `--ct-text-primary` |
| Action label | font (apply all 5) | `--ct-text-body-*` |

**Don't.**
- Don't add a leading icon, avatar, or chevron to the title slot. Section Header has one leading slot — title only (SKILL.md §9.3 spirit).
- Don't hand-type the title in Title Case (`"Scan History"`) or upper case (`"SCAN HISTORY"`). Source naturally and let CSS `capitalize` do the work (SKILL.md §6.5).
- Don't put an icon in the `action` trailing slot. Action is text-only — if a chevron is needed, the variant is `dropdown`, not `action`.
- Don't draw a hairline (`--ct-divider`) above or below the header. The row sits on the same `--ct-bkgd-02` surface as the section beneath it; separation comes from the cream gap above the section, not from a line on the header (SKILL.md §9.2).
- Don't substitute `--ct-bkgd-01` for the container background. The header shares the white sheet with the rows it labels — a cream container would re-introduce the band-style separation the system avoids.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16206-3359) · Master component `16206:3359` · Variant masters: default `17492:13415`, dropdown `17826:13427` (chip `17826:13429`), action `17826:13433` (label `17826:13450`)

### 8. Timeline

**Use.** Vertical progression of steps in a single flow — shows what's done, what's happening now, and what's still ahead. One linear path, one current step at a time. Used for Identity setup, removal progress, and any sequenced task.

**Anatomy.**
```
┌─────────────────────────────────────────────────┐
│  │                                              │   ← top connector (12px, links to previous)
│ ╭───╮                                           │
│ │ ● │   Title                                   │   ← shell (40×40) + body block
│ ╰───╯   Description                             │
│  │                                              │   ← bottom connector (12px, links to next)
└─────────────────────────────────────────────────┘
```
- One row per step. Three slots: leading connector column (2px line + 40×40 shell), body block (title + optional description), no trailing slot.
- The connector column is the shared spine: each row contributes a top segment (above the shell) and a bottom segment (below). First step has no top; last step has no bottom.
- Body block is a `description: boolean` pair — title always shown, description optional.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `completed-first` | Brand-fill shell + check icon, bottom connector brand. No top connector. | First step in the timeline, already done |
| `completed-middle` | Brand-fill shell + check icon, both connectors brand | Middle step, already done |
| `current-middle` | Graph-background shell + timer icon + 40×40 halo overlay, top connector brand, bottom connector graph-background | The active step — exactly one per timeline |
| `upcoming-middle` | Graph-background shell + step-specific feature icon, both connectors graph-background | Middle step, not yet started |
| `upcoming-last` | Graph-background shell + step-specific feature icon, top connector graph-background. No bottom connector. | Last step in the timeline, not yet started |

> _Variant set is intentionally not the full 3×3 (position × state). `completed-last`, `current-first`, `current-last`, `upcoming-first` are not exported in Figma — surface the request rather than improvising one (SKILL.md §7.1, §2.3)._
>
> _Connector colors encode progression as a single rule: a segment is `--ct-brand` when it links a completed-or-current step backward to an already-done step, and `--ct-graph-background` when it links forward into not-yet territory. The boundary is the bottom of the current step._

**Sizing.**
- Container: width 393px; padding-inline `--ct-spacing-20`; padding-block `--ct-spacing-12`; `align-items: center`; `justify-content: space-between`.
- Shell: 40×40 (padding `--ct-spacing-8` around a 24×24 icon); border-radius `--ct-spacing-24`.
- Halo (current-middle only): 40×40, absolute, centered on the shell. Bundled in the SVG asset — no theme token.
- Body block: width 211px (no matching `--ct-spacing-*`; raw value retained until a token lands); `flex-direction: column`; `justify-content: center`; no inter-row gap (line-heights provide it).
- Shell ↔ body gap: `--ct-spacing-12`.
- Connector: 2px wide (no matching `--ct-spacing-2`; raw value retained until a token lands), absolute, vertically centered on the shell column. Visible segment height is 12px above and 12px below the shell — Figma exports completed segments as 32px tall, but the inner 20px sits behind the shell fill and contributes nothing visually. Spec the visible 12px; do not hand-tune the hidden portion.

**Tokens.**

*Container*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |

*Shell*

| Slot | Property | Token |
| --- | --- | --- |
| Shell (`completed-first`, `completed-middle`) | background | `--ct-brand` |
| Shell (`current-middle`, `upcoming-middle`, `upcoming-last`) | background | `--ct-graph-background` |
| Shell icon (`completed-*`) | asset | `informational/check` (24×24) |
| Shell icon (`current-middle`) | asset | `informational/timer` (24×24) + 40×40 halo overlay |
| Shell icon (`upcoming-*`) | asset | step-specific feature icon (24×24, e.g. `feature/identity/email`) |
| Shell icon | color | inherits from shell fill — check on brand, timer/feature on graph-background (no color override) |

*Connector*

| Slot | Property | Token |
| --- | --- | --- |
| Top segment (`completed-middle`, `current-middle`) | background | `--ct-brand` |
| Top segment (`upcoming-middle`, `upcoming-last`) | background | `--ct-graph-background` |
| Bottom segment (`completed-first`, `completed-middle`) | background | `--ct-brand` |
| Bottom segment (`current-middle`, `upcoming-middle`) | background | `--ct-graph-background` |

*Body block*

| Slot | Property | Token |
| --- | --- | --- |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Title | overflow | single-line ellipsis |
| Description | color | `--ct-text-secondary` |
| Description | font (apply all 5) | `--ct-text-body-small-*` |
| Description | overflow | single-line ellipsis |

**Don't.**
- Don't draw the connector with `--ct-divider`. The connector is always `--ct-brand` (done) or `--ct-graph-background` (upcoming) — never the hairline.
- Don't render more than one `current-middle` step in a single timeline. The "current" pointer is singular by design — two halos at once break the linear progression read.
- Don't use `completed-first` for a non-first step, or `upcoming-last` for a non-last step. They omit one connector each; placing them mid-list breaks the visual chain.
- Don't put a check icon on a `current-*` or `upcoming-*` step, or a timer / feature icon on a `completed-*` step. Icon ↔ state is paired 1:1.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17651-5332) · Page `17651:5332` · Variant masters: completed-first `17612:3213`, completed-middle `17612:3249`, current-middle `17612:3212`, upcoming-middle `17612:3211`, upcoming-last `17612:3227`

### 9. Footer

**Use.** End-of-page closures — three distinct moments that wrap a screen: a card-level "see more" link, a global impact band, and a FAQ band. One Footer per closure; not stackable, not interchangeable across the three roles.

**Anatomy.**
```
card-section  ┌─────────────────────────────────────────────────┐
              │  ─────────────────────────────────────────────  │   ← top hairline (0.5px, --ct-divider)
              │                  See details                    │   ← centered text-link, link size
              └─────────────────────────────────────────────────┘

impact        ┌─────────────────────────────────────────────────┐
              │                                                 │
              │              Together, Cloaked users            │   ← line 1, h3 sans
              │           have removed 170 million              │   ← inline Simula on the number, --ct-brand
              │           records from the internet.            │   ← line 3, h3 sans
              │                                                 │
              │             ╭──────────────────╮                │
              │             │  Explore tools   │                │   ← tertiary CTA pill, body sans
              │             ╰──────────────────╯                │
              │                                                 │
              └─────────────────────────────────────────────────┘

faq           ┌─────────────────────────────────────────────────┐
              │  Frequently asked questions                     │   ← Section Header (#7 default, overrides below)
              │                                                 │
              │  ╭───────╮ ╭───────╮ ╭───────╮ ╭───────╮        │   ← horizontal carousel
              │  │Kicker │ │Kicker │ │Kicker │ │Kicker │        │   ← body-small, --ct-brand
              │  │Headln │ │Headln │ │Headln │ │Headln │        │   ← Simula h2-serif, --ct-text-ai-primary
              │  │   →   │ │   →   │ │   →   │ │   →   │        │   ← 48×48 circular icon button
              │  ╰───────╯ ╰───────╯ ╰───────╯ ╰───────╯        │
              │                                                 │   ← bottom padding 240px
              └─────────────────────────────────────────────────┘
```
- `card-section`: one slot — a centered text-link. The top hairline is the only structural element; no leading or trailing slot.
- `impact`: two slots stacked vertically — copy block (3 lines, mixed sans + inline Simula on a single phrase) and tertiary CTA pill. The slot count is fixed.
- `faq`: two slots stacked vertically — Section Header ([Component 7](#7-section-header), `default` variant with overrides documented below) and a horizontally scrolling row of FAQ cards. Each FAQ card is a kit-voice atom: kicker label + Simula headline + circular trailing icon-button.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `card-section` | 50px row, top hairline, centered text-link | Bottom of a card section, leads to a detail view |
| `impact` | 393×550 hero band, centered editorial copy with inline Simula number + tertiary CTA pill | Global app moment ("users have removed N records") after main content |
| `faq` | Fixed-dark AI band, Section Header + horizontal FAQ-card carousel | Bottom of screens with frequently asked questions |

**Sizing.**

*`card-section`*
- Container: width 393px; height 50px (no matching `--ct-spacing-*`; raw value retained until a token lands); padding-inline `--ct-spacing-20`; gap `--ct-spacing-16` (inert with one slot); `align-items: center`; `justify-content: center`.
- Top border: 0.5px (no matching `--ct-spacing-*`; raw value retained until a token lands); solid `--ct-divider`.

*`impact`*
- Container: width 393px; height 550px (no matching `--ct-spacing-*`; raw value retained until a token lands); `overflow: hidden`.
- Inner stack: width 271px (no matching `--ct-spacing-*`; raw value retained until a token lands); horizontally + vertically centered in container; `flex-direction: column`; `align-items: center`; gap `--ct-spacing-32` between copy block and CTA.
- Copy block: width 100% of inner stack; `flex-direction: column`; gap `--ct-spacing-4` between lines; `text-align: center`.
- CTA: intrinsic width; padding-block `--ct-spacing-12`; padding-inline `--ct-spacing-24`; border-radius 100px (no matching `--ct-spacing-*`; pill — raw value retained until a token lands).

*`faq`*
- Container: width 393px; padding-bottom `--ct-spacing-240`; `flex-direction: column`; gap `--ct-spacing-20`; `overflow: hidden`.
- Section Header slot: see [Component 7 — Section Header](#7-section-header) Sizing (padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`).
- Carousel row: padding-inline `--ct-spacing-20`; gap 10px (no matching `--ct-spacing-*`; raw value retained until a token lands) between cards; horizontal scroll.
- FAQ card: width 233px (no matching `--ct-spacing-*`; raw value retained until a token lands); padding-top `--ct-spacing-24`; padding-bottom `--ct-spacing-16`; padding-inline `--ct-spacing-16`; `flex-direction: column`; gap `--ct-spacing-16` between kicker, headline, and icon-button; border-radius `--ct-spacing-20`.
- FAQ card icon-button: 48×48 circular; padding `--ct-spacing-12` around a 24×24 icon (`action/arrow_right`).

**Tokens.**

*`card-section`*

| Slot | Property | Token |
| --- | --- | --- |
| Container | top border | `--ct-divider` |
| Text link | color | `--ct-text-primary` |
| Text link | font (apply all 5) | `--ct-text-link-*` |

*`impact`*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Copy line 1 / line 3 (sans) | color | `--ct-text-primary` |
| Copy line 1 / line 3 (sans) | text-transform | `capitalize` |
| Copy line 1 / line 3 (sans) | font (apply all 5) | `--ct-text-h3-*` |
| Copy "have removed" (sans, inline on line 2) | color | `--ct-text-primary` |
| Copy "have removed" (sans, inline on line 2) | font (apply all 5) | `--ct-text-h3-*` |
| Copy "170 million" (Simula, inline on line 2) | color | `--ct-brand` |
| Copy "170 million" (Simula, inline on line 2) | font (apply all 5) | `--ct-text-h2-serif-*` |
| CTA container | background | `--ct-cta-secondary-container` |
| CTA label | color | `--ct-cta-secondary-text` |
| CTA label | font (apply all 5) | `--ct-text-body-*` |

> _The inline Simula on "170 million" is the **only** sanctioned editorial inline-Simula slot in the system. SKILL.md §2.4 / §6 limits Simula to page titles and FAQ headlines; this slot is an explicit exception ratified by the Figma master to render the impact band as designed. Don't extend the pattern to other inline phrases (see Don't)._

*`faq`*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-ai-input` |
| Section Header container | background | `transparent` (override of [Component 7](#7-section-header) default `--ct-bkgd-02`) |
| Section Header title | color | `--ct-text-ai-primary` (override of [Component 7](#7-section-header) default `--ct-text-primary`) |
| FAQ card | background | fixed-dark surface — no token yet; raw `#1B1B18` (= `--ct-color-grey-04` value). The card sits on the fixed-dark band via `--ct-bkgd-ai-input`, so it cannot use `--ct-bkgd-02` (which flips). Add a `--ct-bkgd-ai-02` token in Figma and re-spec when it lands. |
| FAQ card | border-radius | `--ct-spacing-20` |
| FAQ card kicker | color | `--ct-brand` |
| FAQ card kicker | font (apply all 5) | `--ct-text-body-small-*` |
| FAQ card headline | color | `--ct-text-ai-primary` |
| FAQ card headline | font (apply all 5) | `--ct-text-h2-serif-*` |

> _FAQ headline renders at `--ct-text-h2-serif-*` (24px) per the Figma master, not `--ct-text-h1-serif-*` (32px) as SKILL.md §6.1 currently states — known SKILL.md drift; resolve in a follow-up edit to SKILL.md, not by changing this table or the Figma spec._
>
> _The `faq` band is **fixed dark** via `--ct-bkgd-ai-input` (SKILL.md §5.2). Every text and surface placed on it must also be fixed dark — that is why the Section Header overrides and the FAQ card raw-hex surface exist. Don't substitute `--ct-text-primary` or `--ct-bkgd-02` here; they will flip in light theme and break the band._

**Don't.**
- Don't stack two Footer variants on the same closure (e.g., `card-section` + `impact` back-to-back). The list is positional — one closure per slot. A page may carry an `impact` and a `faq` on different surfaces, but a single section never carries two Footers.
- Don't extend the inline-Simula treatment from `impact` to other phrases ("170 thousand users", "join the waitlist", etc.). The slot is sanctioned for the one impact-number callout that ships with this band; new editorial Simula phrases require a Figma update first (SKILL.md §2.3, §2.4).
- Don't substitute `--ct-bkgd-02` for the FAQ card surface or `--ct-text-primary` for the FAQ headline / Section Header title in the `faq` band. Those tokens flip with theme; the band does not. The result looks correct in dark theme and inverts to white-on-cream in light theme (SKILL.md §5.2).
- Don't add a `chevron.right` to the `card-section` text-link or to the FAQ card. The link is the affordance on `card-section`; the trailing 48×48 icon-button on the FAQ card is the only sanctioned trailing affordance, and it carries an `arrow_right`, not a chevron (SKILL.md §9.3).
- Don't render the Section Header title in title case (`"Frequently Asked Questions"`) or upper case (`"FREQUENTLY ASKED QUESTIONS"`). Source the string naturally (`"frequently asked questions"`) and let the Section Header's `capitalize` rule do the work (SKILL.md §6.5).
- Don't replace the `impact` CTA pill with a primary CTA, a text link, or an icon button. The variant ships with `--ct-cta-secondary-container` for a reason — the pill sits on `--ct-bkgd-01`, where a primary container (`--ct-cta-primary-container` = near-black) would over-weight the band against the editorial copy.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17826-13511) · Page `17826:13511` · Variant masters: card-section `16053:8037`, impact `16196:2887`, faq `17826:15487`

### 10. Navigation

**Use.** Persistent screen chrome — the top bar that anchors a screen and the bottom bar that switches between top-level destinations. Three family members share the *Navigation* schema: `bottom_nav_item` (atomic), `bottom_bar` (composed strip), `top_bar` (page-level header).

**Anatomy.**
```
bottom_nav_item   ╭──────╮
                  │  ⌂   │     ← 24×24 icon in a 12px-padded square; no label
                  ╰──────╯

bottom_bar        ┌─────────────────────────────────────────────────┐
                  │   ⌂      🔍      🔔      👤      ⚙              │   ← 5 items, justify-between
                  └─────────────────────────────────────────────────┘
                       ↑ one item full opacity (selected); others at --ct-opacity-disabled

top_bar / page    ┌─────────────────────────────────────────────────┐
                  │                                                 │   ← 96px top padding (safe-area)
                  │  Activities                                     │   ← Simula H2 title, flex-1
                  └─────────────────────────────────────────────────┘

top_bar / home    ┌─────────────────────────────────────────────────┐
                  │                                                 │   ← 96px top padding (safe-area)
                  │                                         Profile │   ← Body sans, right-aligned
                  └─────────────────────────────────────────────────┘
```
- **bottom_nav_item.** One slot — a 24×24 icon. No label, no badge, no trailing. Selection is encoded in opacity, not in the icon glyph.
- **bottom_bar.** Strip of exactly five `bottom_nav_item`s, `justify-between`, exactly one in `selected` state.
- **top_bar.** One row, two slots — a leading title (active in `page`) and a trailing label (active in `home`). The 96px top padding reserves the iOS safe area; the system draws the status bar at runtime (see Don't).

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `bottom_nav_item/selected` | 24×24 icon at full opacity | The active destination in the bottom bar — exactly one per strip |
| `bottom_nav_item/inactive` | 24×24 icon at `--ct-opacity-disabled` | Every other destination in the same strip |
| `bottom_bar` | White strip of five items, `justify-between`, one selected | Persistent destination switcher pinned to the bottom of every top-level screen |
| `top_bar/page` | Simula H2 title left-aligned, no trailing | Sub-pages that own a name (Activities, Identity, Guard, Monitoring) |
| `top_bar/home` | "Profile" body label right-aligned, no title | The Home screen — no page title, single trailing entry-point |

**Sizing.**

*`bottom_nav_item`*
- Container: padding `--ct-spacing-12` (all sides); intrinsic width = 24 + 12 + 12 = 48px; intrinsic height = 48px.
- Icon: 24×24 (matches the system's standard informational / feature icon size; no spacing token at 24 for icon dimensions, but `--ct-spacing-24` happens to match — reference the icon size as 24×24, not the spacing token).

*`bottom_bar`*
- Container: width 393px (matches the standard screen width used across the system; raw value retained until a screen-width token lands); padding-top `--ct-spacing-16`; padding-bottom `--ct-spacing-24`; padding-inline `--ct-spacing-24`; `flex-direction: column`; `align-items: center`; `justify-content: center`.
- Inner row: width 345px (no matching `--ct-spacing-*`; raw value retained until a token lands — equals 393 − 24 − 24); `justify-content: space-between`; `align-items: center`; five `bottom_nav_item` children. The gap between items is implicit from `space-between`; do not hand-tune it.

*`top_bar`*
- Container: width 393px; padding-top `--ct-spacing-96`; padding-bottom `--ct-spacing-24`; padding-inline `--ct-spacing-16`; `align-items: center`; gap `--ct-spacing-16` (inert on `home`).
- `page` title slot: width 289px (no matching `--ct-spacing-*`; raw value retained until a token lands); single-line.
- `home` trailing slot: width 89px (no matching `--ct-spacing-*`; raw value retained until a token lands); `text-align: right`; container uses `justify-content: flex-end`.

**Tokens.**

*`bottom_nav_item`*

| Slot | Property | Token |
| --- | --- | --- |
| Container (`/selected`) | opacity | `1` (default — no override) |
| Container (`/inactive`) | opacity | `--ct-opacity-disabled` |
| Container | padding | `--ct-spacing-12` |
| Icon | color | inherits from parent text color |

*`bottom_bar`*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | padding-top | `--ct-spacing-16` |
| Container | padding-bottom | `--ct-spacing-24` |
| Container | padding-inline | `--ct-spacing-24` |

*`top_bar`*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | padding-top | `--ct-spacing-96` |
| Container | padding-bottom | `--ct-spacing-24` |
| Container | padding-inline | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-16` |
| Title (`page`) | color | `--ct-text-primary` |
| Title (`page`) | font (apply all 5) | `--ct-text-h2-serif-*` |
| Trailing (`home`) | color | `--ct-text-primary` |
| Trailing (`home`) | font (apply all 5) | `--ct-text-body-*` |

> _Source the page title naturally (`"Activities"`) — `--ct-text-h2-serif-*` does not apply a `text-transform`; the title is rendered as-typed. This is the **page-title slot** sanctioned for Simula in SKILL.md §6.1; do not extend Simula to the `home` Profile label._
>
> _The Figma master exports the `home` Profile slot with a fallback hex of `#f3f1ed` (cream) on the `--global/text/primary` variable — this is a known export quirk; the resolved variable is `--ct-text-primary`, which is what should be referenced. Do not hand-paint Profile in cream._

**Don't.**
- Don't add a chevron, arrow, or label under a `bottom_nav_item`. The icon plus opacity is the entire affordance — labels would re-introduce the chrome the bar deliberately omits (SKILL.md §9.3 spirit).
- Don't differentiate `selected` from `inactive` by swapping to a filled icon variant, adding an underline, or bolding the glyph. Opacity is the only differentiator (SKILL.md §2.5).
- Don't render more than one `selected` item in a single `bottom_bar`. The current-destination pointer is singular — two full-opacity icons break the read.
- Don't use Simula on the `home` Profile label or on any `bottom_nav_item`. Simula is allowed only on the `top_bar/page` title slot in this component (SKILL.md §2.4 / §6.1).
- Don't title-case or upper-case the `page` title (`"ACTIVITIES"`, `"activities"`). The title is rendered as-typed at `--ct-text-h2-serif-*`; source it in the case it should display (`"Activities"`). The `capitalize` rule used by Section Header / Impact does **not** apply here.
- Don't fewer-or-more than five `bottom_nav_item`s in a `bottom_bar`. The strip is fixed at five; if a destination needs to be added or removed, surface the request rather than improvising a 4-up or 6-up variant (SKILL.md §7.1, §2.3).
- Don't introduce a fourth Navigation family member (e.g., `sidebar`, `drawer`, `tabstrip`). The three above are the closed set; `tabstrip` already lives in [Component 5 — Control](#5-control) as `tabs/*` (SKILL.md §7.1, §2.3).
- Don't repurpose `top_bar/home` as a "trailing-only page" template for non-Home screens. The `home` variant is anchored to the Home screen specifically; other screens with a single trailing affordance use a `page` title plus a Section Header action row beneath, not a title-less top bar.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16064-10186) · Page `16064:10186` · Variant masters: bottom_nav_item `16896:6372`, bottom_bar `16896:6679`, top_bar/page `16206:3431`, top_bar/home `16206:3443`

### 11. Card / Feature

**Use.** A small, self-contained surface that snapshots one piece of feature state — a stat, a place, a question, or a long-form automation summary. Sits inside a feature page or band; not a full hero, not a list row.

**Anatomy.**
```
default       ┌──────────────────┐
(activity)    │  ▣                │   ← icon (24×24)
              │                   │
              │  342              │   ← number (h2 sans, capitalize)
              │  Data removal     │   ← label (body-small)
              └──────────────────┘

location      ┌────────────────────┐
              │  ◯ flag             │   ← flag (40×40, full round)
              │  New York,          │   ← city (body)
              │  Dedicated IP       │   ← descriptor (body-small @ 0.5)
              └────────────────────┘

faq           ┌──────────────────────────┐
              │  Call Guard               │   ← kicker (body-small, --ct-brand)
              │                           │
              │  What if I miss           │   ← question (h2-serif, ai-primary)
              │  an important call?       │
              │                           │
              │  ╭───╮                    │
              │  │ → │                    │   ← icon CTA (48×48 secondary)
              │  ╰───╯                    │
              └──────────────────────────┘

automation    ┌────────────────────────────────┐
              │  Essential        3 automations │   ← header: kicker + counter
              │                                 │
              │  Remove from                    │   ← title (h2 sans, capitalize)
              │  major brokers                  │
              ├────────────────────────────────┤
              │  ◯ avatar  Lexisnexis.com       │   ← contact row (avatar + label)
              ├────────────────────────────────┤
              │  ◯ avatar  The Real Yellowpages │
              ├────────────────────────────────┤
              │              See details        │   ← footer (Footer §9 `card-section`)
              └────────────────────────────────┘
```
- **default / location** — one block: leading icon-or-flag + body block (label + value).
- **faq** — three blocks stacked: kicker, question, CTA.
- **automation** — composite of three sections: header (kicker row + title), N contact rows separated by 0.5px hairlines, footer that defers to Footer §9 `card-section`.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `default` (activity) | White surface, 24×24 leading icon, large number + body-small label | Atomic single-stat snapshot — e.g. "342 / Data removal" |
| `location` | Cream surface, 40×40 round flag + city + descriptor (descriptor at raw `opacity: 0.5`) | Locality / IP profile snippet — e.g. "New York / Dedicated IP" |
| `faq` | Dark surface inside the FAQ band, brand-color kicker + Simula question + 48×48 secondary icon CTA (`action/arrow_right`) | FAQ card embedded in the dark FAQ band (SKILL.md §5.2) |
| `automation` | Category-tinted dark surface (`--ct-monitoring-container-02`), composite header + contact rows + card-section footer | Long feature card listing sub-items — e.g. "Remove from major brokers" with broker rows |

**Sizing.**

*default (activity)*
- Container: width 137px (raw — no matching `--ct-spacing-*`); padding `--ct-spacing-16`; border-radius `--ct-spacing-20`; `flex-direction: column`; outer gap **36px raw** (no `--ct-spacing-*` matches; spec'd raw until a token lands); `align-items: flex-start`.
- Icon: 24×24.
- Body block: `flex-direction: column`; gap `--ct-spacing-8`; full width.

*location*
- Container: width 160px (raw); padding `--ct-spacing-16`; border-radius `--ct-spacing-20`; `flex-direction: column`; outer gap `--ct-spacing-12`; `align-items: flex-start`.
- Flag: 40×40, full-round (border-radius ≥ 20px clips to circle).
- Body block: `flex-direction: column`; gap `--ct-spacing-4`; text width 128px (raw; constrained by container interior).

*faq*
- Container: width 233px (raw); padding-top `--ct-spacing-24`; padding-bottom `--ct-spacing-16`; padding-inline `--ct-spacing-16`; border-radius `--ct-spacing-20`; `flex-direction: column`; gap `--ct-spacing-16`; `overflow: clip`.
- Question block: max-height 140px raw (4-line clamp at 24px Simula line-height 1); `text-overflow: ellipsis`.
- CTA: 48×48 (Button_Icon / Secondary — 24×24 arrow inside `--ct-spacing-12` padding on each side).

*automation*
- Outer container: width 314px (raw); padding 0 (children own padding); border-radius `--ct-spacing-20`; `flex-direction: column`.
- Header section: padding `--ct-spacing-16`; gap `--ct-spacing-24`; full width.
  - Kicker row: gap **14px raw** (no `--ct-spacing-*` matches); label width 130px raw; counter width 137px raw, right-aligned; `align-items: center`.
  - Title: full width.
- Contact row: width 314px (raw); padding `--ct-spacing-20`; `justify-content: space-between`; `align-items: center`. Inner cluster (avatar + label) gap `--ct-spacing-12`; avatar 40×40 round; label `flex: 1`, single-line ellipsis. Bottom hairline 0.5px raw (no `--ct-spacing-*` matches), `--ct-divider`.
- Footer section: defers to Footer §9 `card-section` (50px height, top hairline `--ct-divider`, centered link).

**Tokens.**

*default (activity)*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | padding | `--ct-spacing-16` |
| Container | border-radius | `--ct-spacing-20` |
| Number | color | `--ct-text-primary` |
| Number | text-transform | `capitalize` |
| Number | font (apply all 5) | `--ct-text-h2-*` |
| Label | color | `--ct-text-primary` |
| Label | font (apply all 5) | `--ct-text-body-small-*` |

*location* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Container | gap (outer) | `--ct-spacing-12` |
| Body block | gap | `--ct-spacing-4` |
| City | color | `--ct-text-primary` |
| City | font (apply all 5) | `--ct-text-body-*` |
| Descriptor | color | `--ct-text-primary` |
| Descriptor | opacity | `0.5` (raw — only `--ct-opacity-disabled` = 0.3 exists; no match) |
| Descriptor | font (apply all 5) | `--ct-text-body-small-*` |

*faq* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` (resolves dark on the FAQ band — fixed-dark context per SKILL.md §5.2) |
| Container | padding-top | `--ct-spacing-24` |
| Container | padding-bottom | `--ct-spacing-16` |
| Container | padding-inline | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-16` |
| Kicker | color | `--ct-brand` |
| Kicker | font (apply all 5) | `--ct-text-body-small-*` |
| Question | color | `--ct-text-ai-primary` |
| Question | font (apply all 5) | `--ct-text-h2-serif-*` |
| CTA | container | `--ct-cta-secondary-container` |
| CTA | icon color | `--ct-cta-secondary-text` |
| CTA | padding | `--ct-spacing-12` |

> _Question is 24px Simula (`--ct-text-h2-serif-*`), not 32px h1-serif. SKILL.md §6.1 lists the band-level FAQ headline at 32px h1-serif; the embedded card variant uses the smaller 24px (Figma is the source — §1)._

*automation* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-monitoring-container-02` (Category_TBD §9.1) |
| Container | padding | `0` (children own padding) |
| Header | padding | `--ct-spacing-16` |
| Header | gap (between kicker row and title) | `--ct-spacing-24` |
| Kicker label | color | `--ct-text-primary` |
| Kicker label | font (apply all 5) | `--ct-text-body-*` |
| Counter | color | `--ct-text-primary` |
| Counter | text-align | `right` |
| Counter | font (apply all 5) | `--ct-text-body-small-*` |
| Title | color | `--ct-text-primary` |
| Title | text-transform | `capitalize` |
| Title | font (apply all 5) | `--ct-text-h2-*` |
| Contact row | padding | `--ct-spacing-20` |
| Contact row | gap (avatar ↔ label) | `--ct-spacing-12` |
| Contact row | bottom hairline | `--ct-divider`, 0.5px (raw) |
| Contact label | color | `--ct-text-primary` |
| Contact label | font (apply all 5) | `--ct-text-body-*` |
| Footer | spec | defers to [Component 9 — Footer](#9-footer) `card-section` variant |

> _On `automation`, `--ct-text-primary` resolves to the cream value because the card sits in a dark-themed context — the category container is fixed dark per §9.1, but text tokens still come from the active theme._

**Don't.**
- Don't apply `--ct-text-h1-serif-*` (32px) to the FAQ card question. The card-scale FAQ is 24px `--ct-text-h2-serif-*`; the 32px h1-serif belongs to the band-level FAQ headline in Footer §9.
- Don't replace the Automation avatar slot with a generic icon (e.g. `feature/identity/email`). The brand logo is the recognition anchor — generic icons collapse the identity (SKILL.md §9.5).
- Don't pair the Automation footer with a custom "see more" link. Defer to Footer §9 `card-section`; do not duplicate or override its anatomy (SKILL.md §2.3).
- Don't pad the Automation outer container directly. Padding lives on the three child sections; an outer padding adds a second inset that breaks the contact-row's full-width hairline.
- Note: among the four variants, only the FAQ card consumes `--ct-text-ai-*` (it lives on the dark FAQ band); only Automation consumes `--ct-monitoring-/guard-/identity-container-*`. Activity and Location are neutral. (Universal preamble §9.1, §5.2 still applies — these are the sanctioned exceptions for this component.)

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16953-9994) · Page `16953:9994` · Variant masters: default/activity `16061:8390`, location `16061:8391`, faq `16914:7835`, automation `16061:8386`

### 12. Card / Dashboard

**Use.** Atomic dashboard tile that snapshots one feature's state on the home dashboard — a KPI, a status, a scan in progress, an inbox preview, or a wide composite list. One step smaller than a Hero (§13–15), one step larger than a List Item (§6).

**Anatomy.**
```
default                ┌─────────────────┐
(kpi/avators)          │  Created numbers │   ← title (body)
                       │                  │
                       │  5               │   ← number (display-2 sans, 48px)
                       │                  │
                       │  ◯ ◯ ◯           │   ← visualization slot
                       └─────────────────┘

intro                  ┌─────────────────┐
                       │  Authenticator   │   ← title (body)
                       │                  │
                       │  Create a login  │   ← caption (body)
                       │  code that...    │
                       │                  │
                       │  ╭───╮           │   ← Primary icon CTA (16×16 inside spacing-4)
                       │  │ → │           │
                       │  ╰───╯           │
                       └─────────────────┘

scanning               ┌──┬──────────────────────────┐
                       │░░│ Exposure                  │
                       │░░│ Scanning                  │   ← title (body, 2 lines)
                       │░░│                           │
                       │░░│ 28%             20mins    │   ← Display-2 + ETA right
                       └──┴──────────────────────────┘
                         ↑ brand stripe (73×200, --ct-brand)

vpn                    ┌────────────┬───────────────┐
                       │ VPN        │  ◯ ◯ ◯         │
                       │            │   ◯ ◯          │   ← title + Display-2 + Toggle
                       │ On         │ ◯ ◯ ◯ ◯       │     paired with map illustration
                       │ ●─○        │               │
                       └────────────┴───────────────┘

list/digital-risk      ┌────────────────────────────────┐
                       │  Digital risk             High │   ← title (body) + risk word
                       │  ▰▰▰▰▰▰▰▱▱▱▱▱▱▱▱▱             │   ← exposure bar (320×16 SVG)
                       ├────────────────────────────────┤
                       │           See details          │   ← Footer §9 card-section
                       └────────────────────────────────┘

list/recent-activity   ┌────────────────────────────────┐
                       │  Recent activity                │   ← title (body)
                       │░░░Today░░░░░░░░░░░░░░░░░░░░░░░░│   ← Divider §2
                       │  ◯ Lexisnexis              ▓▓░ │   ← Progress row (List Item §6)
                       │░░░Yesterday░░░░░░░░░░░░░░░░░░░░│   ← Divider §2
                       │  ◯ Spokeo            ↑ 4   ▓▓▓│
                       ├────────────────────────────────┤
                       │           See details          │
                       └────────────────────────────────┘

list/actions-taken     ┌────────────────────────────────┐
                       │  Actions taken to protect you   │   ← title (body)
                       │  47       ↑ 4 Today             │   ← Display-2 + Stat (Label §3)
                       │ ────────────────────────────── │
                       │  Removed exposures      342     │   ← stat row (List Item §6)
                       │ ────────────────────────────── │
                       │  Spam blocks            13      │
                       ├────────────────────────────────┤
                       │           See details          │
                       └────────────────────────────────┘

list/inbox             ┌────────────────────────────────┐
                       │  Inbox                       12 │   ← header (body title + count)
                       │  ◯ Lexisnexis           Today  │   ← inbox row (List Item §6)
                       │  ◯ Spokeo               Mon    │
                       │  ◯ Boards.ie            Sun    │
                       └────────────────────────────────┘
```
- **`kpi/*`** — five sub-variants share `default` chrome: header (title + Display-2 number) over a visualization slot. Sub-variants differ only in what fills the visualization slot (see Variants table for each).
- **`intro` / `scanning` / `vpn`** — single-tile variants, anatomy detailed in the Variants table.
- **`list/*`** — wide composites. All four end-defer their row anatomy to List Item §6 and (where applicable) their footer to Footer §9 `card-section`. Per-variant header / row composition in the Variants table.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `kpi/avators` | 173×200 white tile, title + Display-2 number + 3-avatar row in the visualization slot | Created-numbers / login / avatar count KPI (e.g. "Created numbers / 5") |
| `kpi/bars` | …visualization slot is a 7-bar bar chart | Time-series KPI with discrete buckets (e.g. "Block spam calls / 13") |
| `kpi/line` | …visualization slot is a 96px line chart | Time-series KPI with continuous trend (e.g. "Exposure removed / 314") |
| `kpi/pay` | …visualization slot is a 3-stack credit-card illustration | Payment-card count KPI (e.g. "Cloaked Pay / 3") |
| `kpi/status` | Display-2 + body suffix word + Status `/card` pill — no visualization slot | KPI paired with a state label (e.g. "Dark web monitoring / 13 events / Active") |
| `intro` | 173×200 banner-tinted tile, title + caption + Primary icon CTA at bottom | Onboarding lure for an unconfigured feature (e.g. "Authenticator") |
| `scanning` | ~354×200 white tile with `--ct-brand` stripe (73×200) on the left edge; 2-line title + Display-2 percentage + right-aligned ETA | Live scan-in-progress indicator (e.g. "Exposure Scanning / 28%") |
| `vpn` | ~340×200 white tile, title + Display-2 ("On"/"Off") + Toggle paired with 160×168 map illustration | VPN status toggle |
| `list/digital-risk` | 353×var white card; title + risk word (right) + 320×16 exposure bar + card-section footer | Composite "exposure / risk level" indicator |
| `list/recent-activity` | 353×var white card; Divider §2 date bands separating Progress List Item rows; card-section footer | Recent feature events grouped by date |
| `list/actions-taken` | 353×var white card; outer gap `--ct-spacing-40`; header (title + Display-2 + ↑ Stat) + 3 stat rows + card-section footer | Hero KPI with breakdown rows |
| `list/inbox` | 361×var card; header bar (label + count) + N inbox rows; no card-section footer | Compact inbox preview |

**Sizing.**

*default (kpi/avators)*
- Container: width 173px (raw — no matching `--ct-spacing-*`); height 200px (raw); border-radius `--ct-spacing-20`; `flex-direction: column`; `justify-content: space-between`.
- Header block: padding `--ct-spacing-16`; gap `--ct-spacing-12`; `flex-direction: column`; `align-items: flex-start`. Title width 141px (raw — interior constraint).
- Visualization slot: padding-inline `--ct-spacing-16`; padding-block `--ct-spacing-20`; gap `--ct-spacing-8`; avatars 64×64.

*kpi/bars* — visualization slot only
- Padding-block-start `--ct-spacing-4`; padding-block-end `--ct-spacing-20`; padding-inline `--ct-spacing-20`; gap **19px raw** (no `--ct-spacing-*` matches); bars 3×64 raw (illustration).

*kpi/line* — visualization slot only
- Height 96px (raw); full width; `overflow: clip`. Line strokes are illustration, not chrome.

*kpi/pay* — visualization slot only
- Height 109px (raw); credit-card stack is illustration (Mastercard / Spotify / Cloaked card art).

*kpi/status*
- Header block: hero row gap **2px raw** between Display-2 digit and 16px body suffix; suffix width 62px raw.
- Footer block (in place of visualization): padding `--ct-spacing-16`; gap `--ct-spacing-12`; contains a Status `/card` pill (Label §3) — 141px (raw) wide.

*intro*
- Container: 173×200 (same as default); `position: relative` (children absolute-positioned).
- Title: top inset 8% raw, left/right inset 9.09% raw.
- Caption: top inset 31% raw; same left/right inset.
- Primary icon CTA: 24×24 wrapper (icon 16×16 inside `--ct-spacing-4` padding); positioned bottom-center; border-radius 12px raw (resolves to `--ct-spacing-12`).

*scanning*
- Container: 354×200 raw; padding `--ct-spacing-16`; gap `--ct-spacing-8`; `flex-direction: row`; `align-items: center`; `overflow: clip`.
- Brand stripe: position absolute, left 0, top 0, width 73px (raw), height 200px (full bleed).
- Left content column: 161×168 raw; `flex-direction: column`; `justify-content: space-between`.
- Right content column: 160×168 raw; `flex-direction: column`; `align-items: flex-end`; `justify-content: flex-end`.

*vpn*
- Container: padding `--ct-spacing-16`; gap `--ct-spacing-8`; `flex-direction: row`; `align-items: center`.
- Left column: 161×168 raw; `flex-direction: column`; `justify-content: space-between`. Header (title + Display-2): gap `--ct-spacing-12`. Toggle: 72×32 (defers to Control §5).
- Right column: 160×168 raw; `overflow: clip`; border-radius 16px raw (resolves to `--ct-spacing-16`); contains the map illustration.

*list/digital-risk*
- Container: width 353px (raw); border-radius `--ct-spacing-20`; `flex-direction: column`; gap `--ct-spacing-20`; `align-items: center`.
- Header row: padding-top `--ct-spacing-24`; padding-inline `--ct-spacing-16`; `justify-content: space-between`; full width.
- Exposure bar: 320×16 raw (illustration SVG).
- Footer: defers to Footer §9 `card-section` (50px height, top hairline `--ct-divider`).

*list/recent-activity*
- Container: width 353px (raw); border-radius `--ct-spacing-20`; `flex-direction: column`; padding 0 (children own padding); `align-items: flex-start`.
- Header section: padding-block `--ct-spacing-24`; padding-inline `--ct-spacing-16`; gap `--ct-spacing-24`; `flex-direction: column`.
- Date bands: full width — defer to Divider §2.
- Progress rows: full width — defer to List Item §6 progress variant.
- Footer: defers to Footer §9 `card-section`.

*list/actions-taken*
- Container: width 353px (raw); border-radius `--ct-spacing-20`; `flex-direction: column`; outer gap `--ct-spacing-40`.
- Header section: padding-top `--ct-spacing-24`; padding-inline `--ct-spacing-16`; gap `--ct-spacing-24`; `flex-direction: column`.
- Hero row: gap `--ct-spacing-16`; `align-items: flex-end`. Number block 113px raw; gap **2px raw** between Display-2 digit and trailing element.
- Stat rows: width 322px (raw — interior gutter); padding-block `--ct-spacing-16`; bottom hairline 0.5px raw, `--ct-divider`. Defers to List Item §6 stat variant.
- Footer: width 337px raw; defers to Footer §9 `card-section`.

*list/inbox*
- Container: width 361px (raw); border-radius `--ct-spacing-20`; `flex-direction: column`; `overflow: clip` (rounds the corners on row backgrounds).
- Header bar: padding `--ct-spacing-16`; `justify-content: space-between`; full width.
- Inbox rows: padding `--ct-spacing-20`; defer anatomy to List Item §6 inbox variant.

**Tokens.**

*default (kpi/avators)*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | border-radius | `--ct-spacing-20` |
| Header block | padding | `--ct-spacing-16` |
| Header block | gap | `--ct-spacing-12` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Number | color | `--ct-text-primary` |
| Number | font (apply all 5) | `--ct-text-display-2-*` |
| Visualization slot | padding-inline | `--ct-spacing-16` |
| Visualization slot | padding-block | `--ct-spacing-20` |
| Visualization slot | gap | `--ct-spacing-8` |

*kpi/bars / kpi/line / kpi/pay* — chrome matches `default`. Visualization geometry (bar widths, line strokes, card art) is illustration, not chrome — no token table. The `kpi/pay` illustration uses raw brand colors (`#f56600`, `#1ed760`) intentionally for asset recognition; do not tokenize.

*kpi/status* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Suffix word | color | `--ct-text-primary` |
| Suffix word | font (apply all 5) | `--ct-text-body-*` |
| Status pill block | padding | `--ct-spacing-16` |
| Status pill block | gap | `--ct-spacing-12` |
| Status pill | spec | defers to [Component 3 — Label](#3-label) `status/card` variant |

*intro* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-banner-container` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Caption | color | `--ct-text-primary` |
| Caption | font (apply all 5) | `--ct-text-body-*` |
| Primary icon CTA | container | `--ct-cta-primary-container` |
| Primary icon CTA | icon color | `--ct-cta-primary-text` |
| Primary icon CTA | padding | `--ct-spacing-4` |

*scanning* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | padding | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-8` |
| Brand stripe | background | `--ct-brand` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Number | color | `--ct-text-primary` |
| Number | font (apply all 5) | `--ct-text-display-2-*` |
| ETA | color | `--ct-text-primary` |
| ETA | font (apply all 5) | `--ct-text-body-*` |

*vpn* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | padding | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-8` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Number ("On" / "Off") | font (apply all 5) | `--ct-text-display-2-*` |
| Toggle | spec | defers to [Component 5 — Control](#5-control); on-state container resolves to `--ct-status-success-solid` |
| Map illustration column | background | `--ct-bkgd-01` |

> _The Figma master references the `--ct-color-green-01` primitive on the on-state Toggle. Per SKILL.md §4.4, components consume the semantic token (`--ct-status-success-solid`), not the primitive — both resolve to the same hex._

*list/digital-risk* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | padding-top | `--ct-spacing-24` |
| Container | padding-inline | `--ct-spacing-16` |
| Container | gap | `--ct-spacing-20` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Risk word | color | _TBD_ |
| Risk word | font (apply all 5) | `--ct-text-body-*` |
| Footer | spec | defers to [Component 9 — Footer](#9-footer) `card-section` variant |

> _Risk-word color in Figma is raw `#c90004`. The closest existing token, `--ct-status-fail-solid` (`#b83100`), does not match — it's a different red. Add a darker fail-status token in Figma and re-export before resolving this slot. Per SKILL.md §2.1, do not substitute the closest token by hand._

*list/recent-activity* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Header | padding-block | `--ct-spacing-24` |
| Header | padding-inline | `--ct-spacing-16` |
| Header | gap | `--ct-spacing-24` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Date band | spec | defers to [Component 2 — Divider](#2-divider) |
| Progress row | spec | defers to [Component 6 — List Item](#6-list-item) progress variant |
| Footer | spec | defers to [Component 9 — Footer](#9-footer) `card-section` variant |

*list/actions-taken* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | gap (outer) | `--ct-spacing-40` |
| Header | padding-top | `--ct-spacing-24` |
| Header | padding-inline | `--ct-spacing-16` |
| Header | gap (between title and hero row) | `--ct-spacing-24` |
| Title | color | `--ct-text-primary` |
| Title | font (apply all 5) | `--ct-text-body-*` |
| Hero row | gap (between number and Stat) | `--ct-spacing-16` |
| Number | color | `--ct-text-primary` |
| Number | font (apply all 5) | `--ct-text-display-2-*` |
| Stat pill | spec | defers to [Component 3 — Label](#3-label) `stat/up` variant |
| Stat row | padding-block | `--ct-spacing-16` |
| Stat row | bottom hairline | `--ct-divider`, 0.5px (raw) |
| Stat row | spec | defers to [Component 6 — List Item](#6-list-item) stat variant |
| Footer | spec | defers to [Component 9 — Footer](#9-footer) `card-section` variant |

*list/inbox* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | none (children own background) |
| Header bar | background | `--ct-bkgd-02` |
| Header bar | padding | `--ct-spacing-16` |
| Header label | color | `--ct-text-primary` |
| Header label | font (apply all 5) | `--ct-text-body-*` |
| Inbox row | background | `--ct-bkgd-02` |
| Inbox row | padding | `--ct-spacing-20` |
| Inbox row | spec | defers to [Component 6 — List Item](#6-list-item) inbox variant |

**Don't.**
- Don't add a card-section footer to `list/inbox`. The Figma master ends at the last inbox row; adding a "See details" footer drifts from spec (SKILL.md §2.3).
- Don't replace the `intro` banner background with `--ct-bkgd-02` "for consistency." The `--ct-banner-container` cream tint is the visual signature that marks `intro` as the unconfigured-feature lure (SKILL.md §9.5 spirit).
- Don't pad the `list/inbox` outer container directly. Padding lives on the header bar and on each inbox row; an outer pad creates a second inset that breaks the row's full-width hairline.

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16063-9308) · Page `16063:9308` · Variant masters: kpi/avators `16906:7329`, kpi/bars `16906:7234`, kpi/line `16901:7057`, kpi/pay `16906:7386`, kpi/status `16901:7027`, intro `16022:5191`, scanning `16910:7549`, vpn/off `16910:7499`, vpn/on `16910:7500`, list/digital-risk `17384:8997`, list/recent-activity `17384:8995`, list/actions-taken `17384:8996`, list/inbox `16238:5139`

### 13. Hero / Feature

**Use.** Full-width feature face at the top of a feature page — a single hero "moment" that introduces, summarizes, or visualizes a feature. Three patterns share the *Hero / Feature* schema: **intro** (illustration + title + Primary CTA — onboarding lure), **active** (header stat + visualization or detail card — live / configured state), and **scanning** (full-bleed media + status footer — work-in-progress state). Pick the pattern by the feature's lifecycle stage.

**Anatomy.**
```
intro/call-guard      ┌────────────────────────────┐
                      │   ☎ illustration            │   ← banner-tinted top, raster asset
                      ├────────────────────────────┤
                      │  Set up · 2 minutes        │   ← kicker row (body-small)
                      │  Block suspicious calls    │   ← title (h1 sans, capitalize)
                      │  in real time              │
                      │  ╭──────────────────────╮  │
                      │  │  Set up Call Guard   │  │   ← Primary CTA (full-width)
                      │  ╰──────────────────────╯  │
                      └────────────────────────────┘

intro/vpn             ┌────────────────────────────┐
                      │                       ╭─╮  │   ← top-right expand button
                      │   · · · · · ·         ╰─╯  │   ← world map + 11 dots
                      │ · · · · · · · · ·          │
                      │   · · · · · ·              │
                      │  Your Internet,            │   ← title (h1 sans, capitalize)
                      │  But More Private          │
                      │  ╭──────────────────────╮  │
                      │  │ Secure my connection │  │   ← Primary CTA, monitoring tint
                      │  ╰──────────────────────╯  │
                      └────────────────────────────┘

intro/identity        ┌────────────────────────────┐
                      │░░░ raw dark gradient    ░░░│   ← gradient (illustration)
                      │░░░ photo overlay (screen)░░│   ← raster, mix-blend: screen
                      │░░░ "Hide Email" video    ░░│   ← autoplay, mix-blend: lighten
                      │  Never give away your      │   ← title (h1 sans, capitalize, cream)
                      │  real information again    │
                      │  ╭──────────────────────╮  │
                      │  │   Get Started        │  │   ← Primary CTA (inverted: cream / dark)
                      │  ╰──────────────────────╯  │
                      └────────────────────────────┘

active/call-guard     ┌────────────────────────────┐
                      │  Calls Blocked              │   ← label (h3 sans, capitalize)
                      │  324                        │   ← number (display-1, 72px)
                      │  ┌──────────────────────┐  │
                      │  │ ▆▆ ▆ ▆ ▆ ▆ ▆ ▆ ▆     │  │   ← 9-bar bar chart card
                      │  │ M T W T F S S        │  │
                      │  │ ╭──╮ ╭──╮ ╭──╮       │  │
                      │  │ │Wk│ │Mn│ │Yr│       │  │   ← Segment control
                      │  │ ╰──╯ ╰──╯ ╰──╯       │  │
                      │  └──────────────────────┘  │
                      └────────────────────────────┘

active/data-removal   ┌────────────────────────────┐
                      │  Total Removed   ╭────────╮ │
                      │                  │•Next…  │ │   ← label (h3) + Status pill
                      │  276             ╰────────╯ │   ← number (display-1)
                      │                            │
                      │  Email   ▰▰▰▰▰▰         24 │   ← 5-row category bar list
                      │  Family  ▰▰              32 │
                      │  Name    ▰▰▰▰            21 │
                      │  Phone   ▰▰              17 │
                      │  Address ▰▰▰▰▰▰▰▰        58 │
                      │                            │
                      │  ▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮  │   ← stacked-area chart (illustration)
                      │  Mar 1                Today │
                      └────────────────────────────┘

active/vpn            ┌────────────────────────────┐
                      │   · · · · · · ·       ╭─╮  │
                      │ · · · · · · · · ·     ╰─╯  │   ← map (top) + expand button
                      ├────────────────────────────┤
                      │  Connected      03:45:82   │   ← timer row (body)
                      │  ─────────────────────────  │
                      │  Service       New York 🇺🇸 │   ← service row + flag avatar
                      │  ╭──────────────────────╮  │
                      │  │     Disconnect       │  │   ← Primary CTA
                      │  ╰──────────────────────╯  │
                      └────────────────────────────┘

scanning/data-removal ┌────────────────────────────┐
                      │░░░ raw photo + brand    ░░░│   ← orange mix-blend: multiply
                      │░░░ counter video        ░░░│   ← autoplay, mix-blend: lighten
                      │       Places data is       │   ← caption (body, cream)
                      │       exposed              │
                      │  Started 10mins   ╭──────╮ │
                      │  ago              │•22:24│ │   ← Status pill (status/active)
                      │                   ╰──────╯ │
                      └────────────────────────────┘
```
- **`intro/*`** — three sub-variants. All share an *intro* face: full-bleed illustration column on top + text block (optional kicker row → title → Primary CTA) below.
  - `intro/call-guard` — banner-tinted illustration band + kicker row + 2-line H1 title + full-width Primary CTA.
  - `intro/vpn` — full-bleed dotted world map + top-right `ButtonIconPrimary` (expand glyph) + 2-line H1 title + Primary CTA tinted with `--ct-monitoring-container-02`.
  - `intro/identity` — full-bleed dark gradient + screen-blended photo overlay + lighten-blended autoplay video + 2-line H1 title (cream) + cream Primary CTA. Hero requires `data-theme="dark"` context (SKILL.md §5.1).
- **`active/*`** — three sub-variants. All share an *active* face: stat header (H3 label + Display-1 number) + visualization or detail.
  - `active/call-guard` — Bar chart card (9 raw-px bars) + Segment control (Week / Month / Year).
  - `active/data-removal` — Header pairs Display-1 with a `Status` pill (Component 3 `status/card`); body is a 5-row category bar list + a stacked-area time-series chart.
  - `active/vpn` — Map fills the top; bottom is a white detail card with a Connected timer row, a Service row (label + `Avatar_Flags` instance), and a "Disconnect" Primary CTA.
- **`scanning/*`** — one sub-variant. Full-bleed photo + `--ct-brand` orange `mix-blend-multiply` overlay + autoplay counter video + caption + footer Status pill.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `intro/call-guard` (default) | 393×~525 banner-tinted hero, raster illustration top + kicker row + H1 title + full-width Primary CTA | Onboarding / unconfigured-feature lure for Call Guard |
| `intro/vpn` | 393×543 cream hero, full-bleed world map (decorative) with 11 dot markers + top-right expand button + H1 title + Primary CTA tinted with `--ct-monitoring-container-02` | Onboarding lure for VPN — brand-purple CTA marks it as a VPN-product moment |
| `intro/identity` | 393×756 dark-gradient hero, raster photo overlay (screen blend) + autoplay video (lighten blend) + cream H1 title + cream Primary CTA | Onboarding / first-launch hero for the Identity product (requires `data-theme="dark"` per §5.1) |
| `active/call-guard` | 394×~600 white hero (1px wider than the rest — preserve), H3 label + Display-1 hero number + 9-bar chart card + Segment control | Active Call-Guard state — KPI ("324 / Calls Blocked") with weekly trend |
| `active/data-removal` | 393×~600 white hero, H3 label + Display-1 number + Status pill + 5-row category bar list + stacked-area chart | Active Data-Removal state — totals + per-category progress + time-series |
| `active/vpn` | 393×468 cream hero, top half is a map; bottom half is a detail card with timer + Service+flag + Disconnect Primary CTA | Active VPN connection — location, uptime, and disconnect affordance |
| `scanning/data-removal` | 393×521 black hero, full-bleed raster photo + `--ct-brand` mix-blend-multiply + autoplay counter video + caption + Status pill (`status/active`) | Scan-in-progress state for Data Removal — replaces "Loading…" with a heroed live state |

**Sizing.**

*intro/call-guard (default)*
- Container: width 393px (raw — no matching `--ct-spacing-*`); height intrinsic; `flex-direction: column`; `align-items: stretch`. Children own padding (no outer pad).
- Illustration band: width 100%; height 333px (raw — illustration height; do not tokenize). Hosts a 225.5×220px raster asset (raw — illustration geometry).
- Text block: padding-block `--ct-spacing-24`; padding-inline `--ct-spacing-20`; gap `--ct-spacing-24`; full width.
  - Kicker row: `flex-direction: row`; `align-items: center`; gap **10px raw** (no `--ct-spacing-*` matches). Bullet dot 6×6 (illustration).
  - Title: full width.
  - CTA: defers to [Component 1 — Button](#1-button) `text/primary` (height 56px, full-width, padding `--ct-spacing-16`, border-radius `--ct-spacing-16`).

*intro/vpn* — overrides
- Container: width 393px (raw); height 543px (raw — outer hero height fixed by illustration); `position: relative` (children absolutely positioned over the map); `overflow: clip`.
- Map illustration: position absolute, full bleed; `bottom: 47px` raw; `left: -525px` raw; `width: 966px` raw; `height: 600px` raw; `opacity: 0.5` (raw — illustration; no `--ct-opacity-*` match).
- 11 dot markers: each 8×8, raw absolute coordinates (illustration; do not tokenize).
- Top-right expand button: position absolute; `top: var(--ct-spacing-16)`; `right: var(--ct-spacing-16)` (the spec board renders this as `left: 329px, top: 16px` on a 393px container — equivalent). Defers to [Component 1 — Button](#1-button) `icon-primary/default`.
- Text block: pinned to the bottom of the container; padding-block `--ct-spacing-24`; padding-inline `--ct-spacing-20`; gap `--ct-spacing-24`. No kicker row.
- CTA: same `text/primary` geometry; container token swaps to `--ct-monitoring-container-02` (Category_TBD §9.1).

*intro/identity* — overrides
- Container: width 393px (raw); height 756px (raw); `position: relative`; `overflow: clip`.
- Background: raw dual gradient (illustration; do not tokenize). See Tokens.
- Photo overlay: position absolute; `left: -172px` raw; `top: 190px` raw; `width: 736px` raw; `height: 919px` raw; `mix-blend-mode: screen`; `opacity: 0.9` raw.
- Animation video: position absolute; `left: 0`; `top: 324px` raw; `width: 393px` raw; `height: 110px` raw; `mix-blend-mode: lighten`; `<video autoPlay loop muted playsInline>`.
- Text block: pinned to the bottom (`top: 567px` raw); padding-block `--ct-spacing-24`; padding-inline `--ct-spacing-20`; gap `--ct-spacing-24`. No kicker.
- CTA: `text/primary` geometry; container / label resolve to inverted dark-theme values — see Tokens.

*active/call-guard* — overrides
- Container: width 394px (raw — 1px wider than the rest; preserve, do not normalize); height intrinsic; `flex-direction: column`; gap `--ct-spacing-24`; `align-items: flex-start`.
- Header block: padding-top `--ct-spacing-24`; padding-inline `--ct-spacing-20`; padding-bottom `--ct-spacing-20`; gap `--ct-spacing-24`; full width; `flex-direction: column`.
- Chart card: full width; padding `--ct-spacing-20`; gap `--ct-spacing-24`; `align-items: center`; `flex-direction: column`.
  - Bar chart: 354×238px raw (illustration container); 9 bar columns at 16×{100..184}px raw (illustration heights vary per data); 8 hairline separators between bars (`--ct-divider`, 0.5px raw). Day labels (`M T W T F S S`).
  - Segment control: width 354px raw; gap `--ct-spacing-16`; three Segment items at 107 / 108 / 107 px (raw); each item padding **10px raw** + `--ct-spacing-12` (block + inline); border-radius `--ct-spacing-16`. (No standalone Segment Control spec exists yet; geometry inlined here. When one lands, defer to it.)

*active/data-removal* — overrides
- Container: width 393px (raw); padding-block `--ct-spacing-40`; gap `--ct-spacing-40`; `align-items: center`; `flex-direction: column`.
- Stats column: width 354px raw; gap `--ct-spacing-40`; `flex-direction: column`.
  - Header row: full width; `flex-direction: row`; `align-items: flex-end`; `justify-content: space-between`. Title block (left): `flex-direction: column`; gap `--ct-spacing-24`; width 173px raw. Status pill (right): width 148px raw — defers to [Component 3 — Label](#3-label) `status/card`.
  - Category bar list: gap `--ct-spacing-4`; full width. Each row: `flex-direction: row`; gap `--ct-spacing-8`; `align-items: center`. Cells: label 83px raw, bar 208×3px raw (track + fill, raw category hexes — see Tokens), count 47px raw right-aligned.
- Stacked-area chart: full width; height 233px raw; `overflow: clip`. Inner cluster 353px raw wide (illustration). Axis labels: "Mar 1" 36.588px raw, "Today" 154.542px raw at `opacity: 0.7` raw (illustration / chart geometry; do not tokenize).

*active/vpn* — overrides
- Container: width 393px (raw); height 468px (raw); `position: relative`; `overflow: clip`.
- Map: position absolute; `right: 0`; `top: -157px` raw; `width: 1622px` raw; `height: 1008px` raw (zoomed map detail with two `mix-blend-multiply` location markers — 50px outer pulse + 10px inner dot, raw illustration).
- Top-right expand button: position absolute; `top: var(--ct-spacing-16)`; `right: var(--ct-spacing-16)`. Defers to [Component 1 — Button](#1-button) `icon-primary/default`.
- Detail card: position absolute; `bottom: 0`; full width; padding-inline `--ct-spacing-20`; padding-bottom `--ct-spacing-40`; padding-top `0` (the Connected row owns its top padding); `flex-direction: column`; `align-items: flex-start`.
  - Connected row: padding-block `--ct-spacing-24`; full width; `flex-direction: row`; `justify-content: space-between`; `align-items: center`. Right cell ("03:45:82") width 129px raw, right-aligned.
  - Hairline divider: full width, `--ct-divider`, 0.5px raw.
  - Service row: padding-block `--ct-spacing-20`; full width; `flex-direction: row`; `justify-content: space-between`; `align-items: center`. Right cluster 114×20px raw — text "New York" + `Avatar_Flags` instance (40×40, full round) wrapping a 34×18px raster flag asset (`flag/America`; raw illustration).
  - CTA: defers to [Component 1 — Button](#1-button) `text/primary` ("Disconnect").

*scanning/data-removal* — overrides
- Container: width 393px (raw); height 521px (raw); `position: relative`; `overflow: clip`.
- Photo + overlay: position absolute; `left: 0`; `top: 0`; `width: 393.333px` raw; `height: 521.111px` raw (sub-pixel offsets are illustration geometry; do not normalize). Photo is a raster asset; the orange overlay sits on top with `mix-blend-mode: multiply`.
- Counter video: position absolute; `left: 0`; `top: 191px` raw; `width: 149px` raw; `height: 149px` raw; `mix-blend-mode: lighten`; `<video autoPlay loop muted playsInline>`.
- Caption: position absolute; `top: 298.89px` raw; horizontally centered; `text-align: center`.
- Footer status row: position absolute; `left: 16.67px` raw; `top: 474px` raw; `width: 360.334px` raw; `flex-direction: row`; `align-items: center`; `justify-content: space-between`. Right slot hosts a `Status` pill (Component 3) — `status/active` variant.

**Tokens.**

*intro/call-guard (default)*

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-banner-container` |
| Illustration band | background | `--ct-banner-container` (inherits from container; the asset itself is raster, not chrome) |
| Text block | padding-block | `--ct-spacing-24` |
| Text block | padding-inline | `--ct-spacing-20` |
| Text block | gap | `--ct-spacing-24` |
| Kicker label | color | `--ct-text-primary` |
| Kicker label | font (apply all 5) | `--ct-text-body-small-*` |
| Title | color | `--ct-text-primary` |
| Title | text-transform | `capitalize` |
| Title | font (apply all 5) | `--ct-text-h1-*` |
| CTA | spec | defers to [Component 1 — Button](#1-button) `text/primary` |

*intro/vpn* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Top-right expand button | spec | defers to [Component 1 — Button](#1-button) `icon-primary/default` |
| CTA | container | `--ct-monitoring-container-02` (Category_TBD §9.1) |
| CTA | label color | `--ct-cta-primary-text` |

*intro/identity* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | _TBD_ — raw dual gradient (`linear-gradient(180deg, #0a0a0a 8.69%, #353d45 50.30%, #ccced1 137.05%)` over `linear-gradient(90deg, #194945, #194945)`); illustration only — do not tokenize |
| Photo overlay | mix-blend-mode | `screen` (raw — illustration) |
| Photo overlay | opacity | `0.9` (raw — only `--ct-opacity-disabled` = 0.3 exists; no match) |
| Video overlay | mix-blend-mode | `lighten` (raw — illustration) |
| Title | color | `--ct-text-primary` (resolves cream when hero is in `data-theme="dark"` — see note) |
| CTA | container | `--ct-cta-primary-container` (resolves cream under `data-theme="dark"`) |
| CTA | label color | `--ct-cta-primary-text` (resolves dark under `data-theme="dark"`) |

> _`intro/identity` requires `data-theme="dark"` on its hero root. Under light theme, `--ct-cta-primary-container` resolves to black and `--ct-text-primary` resolves to dark — both wrong against the dark gradient. The Figma master is captured under the dark-theme override; do not hard-code the cream values._

*active/call-guard* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | gap (outer) | `--ct-spacing-24` |
| Header block | padding-top | `--ct-spacing-24` |
| Header block | padding-inline | `--ct-spacing-20` |
| Header block | padding-bottom | `--ct-spacing-20` |
| Header block | gap | `--ct-spacing-24` |
| Label | color | `--ct-text-primary` |
| Label | text-transform | `capitalize` |
| Label | font (apply all 5) | `--ct-text-h3-*` |
| Number | color | `--ct-text-primary` |
| Number | font (apply all 5) | `--ct-text-display-1-*` |
| Chart card | padding | `--ct-spacing-20` |
| Chart card | gap | `--ct-spacing-24` |
| Bar chart bars | fill | _TBD_ — color-baked in SVG; same caveat as Component 1 §icon strokes — Figma must export the bar fill as a variable for theme-aware re-color |
| Bar separators | stroke | `--ct-divider`, 0.5px (raw) |
| Day label | color | `--ct-text-primary` |
| Day label | opacity | `0.6` (raw — only `--ct-opacity-disabled` = 0.3 exists; no match) |
| Day label | font (apply all 5) | `--ct-text-link-*` |
| Segment control | gap | `--ct-spacing-16` |
| Segment item / selected | background | `--ct-cta-primary-container` |
| Segment item / selected | label color | `--ct-cta-primary-text` |
| Segment item / unselected | border-color | `--ct-cta-secondary-container` |
| Segment item / unselected | label color | `--ct-text-primary` |
| Segment item | padding | **10px raw** + `--ct-spacing-12` (block + inline; no `--ct-spacing-10`) |
| Segment item | border-radius | `--ct-spacing-16` |
| Segment item | label font (apply all 5) | `--ct-text-link-*` |

*active/data-removal* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-02` |
| Container | padding-block | `--ct-spacing-40` |
| Container | gap (outer) | `--ct-spacing-40` |
| Stats column | gap | `--ct-spacing-40` |
| Title block (left) | gap | `--ct-spacing-24` |
| Label | color | `--ct-text-primary` |
| Label | text-transform | `capitalize` |
| Label | font (apply all 5) | `--ct-text-h3-*` |
| Number | color | `--ct-text-primary` |
| Number | font (apply all 5) | `--ct-text-display-1-*` |
| Status pill | spec | defers to [Component 3 — Label](#3-label) `status/card` ("Next scan Oct 12") |
| Category row | gap (label↔bar↔count) | `--ct-spacing-8` |
| Category row label / count | color | `--ct-text-primary` |
| Category row label / count | font (apply all 5) | `--ct-text-body-*` |
| Category bar track | background | `--ct-bkgd-02` |
| Category bar fill (Email) | background | _TBD_ — raw `#00c49a` (no token; not in Category_TBD set) |
| Category bar fill (Family) | background | _TBD_ — raw `#faa542` (no token) |
| Category bar fill (Name) | background | _TBD_ — raw `#719a03` (no token) |
| Category bar fill (Phone) | background | _TBD_ — raw `#e1473f` (no token) |
| Category bar fill (Address) | background | _TBD_ — raw `#003ab8` (no token) |
| Stacked-area chart | bands | _TBD_ — same five raw category hexes as above; chart is illustration |
| Axis label | color | `--ct-text-primary` |
| Axis label | opacity | `0.7` (raw — no token) |
| Axis label | font (apply all 5) | `--ct-text-link-*` |

> _The five category-bar hexes (`#00c49a, #faa542, #719a03, #e1473f, #003ab8`) are not in `tokens/colors.css`, are not Category_TBD members, and are not exported as Figma variables. Per SKILL.md §2.1, do not approximate with the closest existing token; surface a request to add a category-color palette to Figma and re-export before resolving these slots._

*active/vpn* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-01` |
| Map illustration | spec | raw — decorative, do not tokenize |
| Top-right expand button | spec | defers to [Component 1 — Button](#1-button) `icon-primary/default` |
| Detail card | background | `--ct-bkgd-02` |
| Detail card | padding-inline | `--ct-spacing-20` |
| Detail card | padding-bottom | `--ct-spacing-40` |
| Connected row | padding-block | `--ct-spacing-24` |
| Connected row label / value | color | `--ct-text-primary` |
| Connected row label / value | font (apply all 5) | `--ct-text-body-*` |
| Hairline divider | stroke | `--ct-divider`, 0.5px (raw) |
| Service row | padding-block | `--ct-spacing-20` |
| Service row label / value | color | `--ct-text-primary` |
| Service row label / value | font (apply all 5) | `--ct-text-body-*` |
| Flag avatar (`Avatar_Flags / flag/America`) | spec | raw — flag asset is raster, do not tokenize |
| CTA | spec | defers to [Component 1 — Button](#1-button) `text/primary` ("Disconnect") |

> _The Figma `active/vpn` master binds the CTA label color to `--ct-bkgd-02` (white) instead of `--ct-cta-primary-text` (also white in light theme). Both resolve to the same hex today, but the spec consumes `--ct-cta-primary-text` per the Button §1 contract — do not hard-code the surface token for the label._

*scanning/data-removal* — overrides

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | _TBD_ — raw `#000`; no `--ct-bkgd-*` resolves to pure black (light `--ct-bkgd-01` = cream, dark `--ct-bkgd-01` = `grey-05` ≠ pure black). Do not substitute `--ct-color-black` (a primitive — components consume semantic tokens only per SKILL.md §4.4) |
| Photo | spec | raw raster, illustration — do not tokenize |
| Orange overlay | background | `--ct-brand` |
| Orange overlay | mix-blend-mode | `multiply` (raw — illustration) |
| Counter video | mix-blend-mode | `lighten` (raw — illustration) |
| Caption | color | `--ct-text-primary` (resolves cream when hero is in `data-theme="dark"` — see note) |
| Caption | text-align | `center` |
| Caption | font (apply all 5) | `--ct-text-body-*` |
| Footer status label ("Started 10mins ago") | color | `--ct-text-primary` (cream under `data-theme="dark"`) |
| Footer status label | font (apply all 5) | `--ct-text-body-*` |
| Status pill | spec | defers to [Component 3 — Label](#3-label) `status/active` |

> _The black surface is rendered raw in Figma — there is no `--ct-bkgd-*` token that resolves to pure `#000`. Until Figma adds a primitive that maps to pure black (or a dedicated `--ct-bkgd-scanning` token), mark the surface TBD. The variant lives on a fixed-dark surface, so the hero must be wrapped in `data-theme="dark"` for `--ct-text-primary` to flip cream._

**Don't.**
- Don't substitute `--ct-cta-primary-container` (black) for the `intro/vpn` CTA "to use the standard token." The brand-purple CTA is the visual signature that marks this hero as VPN; `--ct-monitoring-container-02` is the only sanctioned override (SKILL.md §9.1, §9.5).
- Don't replace the `intro/vpn` map, the `intro/call-guard` raster illustration, the `scanning/data-removal` photo, or the `intro/identity` photo+video with a generic icon. Each is the feature's visual signature and the recognition anchor for that hero (SKILL.md §9.5).
- Don't pad the `active/vpn` detail card from above. The Connected row owns its own `--ct-spacing-24` top padding; an outer top-pad creates a second inset that breaks the row rhythm.
- Don't render `intro/identity` under `data-theme="light"` and hard-code cream colors to compensate. The hero must sit in `data-theme="dark"` so the existing `--ct-cta-primary-*` and `--ct-text-primary` tokens flip naturally (SKILL.md §5.1).

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17826-13477) · Specimen frame `17826:13477` · Variant masters: intro/call-guard `16914:7971`, intro/vpn `16914:8028`, intro/identity `17794:9999`, active/call-guard `16914:7849`, active/data-removal `16675:11615`, active/vpn `16206:3353`, scanning/data-removal `16206:3354`

### 14. Hero / Kit Briefing

**Use.** Full-screen AI moment — Cloaked's Kit (AI persona) acknowledges the user's input in editorial voice and surfaces a single recommended action card. One pattern, one face: a Simula headline floating over a dark sheet with a decorative orange blob, anchored by an AI notification card with an animated guard avatar. Reach for it as the AI handoff face after a user prompt, not as a generic recommendation surface.

**Anatomy.**
```
┌────────────────────────────┐
│      ░░░ orange blob ░░░    │   ← decorative SVG (top, off-canvas, blurred)
│   ░░░░░░░░░░░░░░░░░░░░░░    │
│                            │
│                            │
│  Got it. Let's look at     │   ← Simula H1 headline (cream, 2 lines)
│  your data instead.        │
│                            │
│  ╭──────────────────────╮  │
│  │ ◉  Block spam calls  │  │   ← AI notification card (fixed-dark)
│  │    Peace in 30 secs  │  │      avatar (40×40, animated) + 2-line text
│  ╰──────────────────────╯  │
│                            │
└────────────────────────────┘
```
- **Outer face.** A single dark sheet — the floor uses `--ct-bkgd-ai-input` (fixed-dark, AI token). The hero sits on `data-theme="dark"` so the inner sheet, headline, and label colors flip cream.
- **Components sheet.** Full-bleed `--ct-bkgd-02` (resolves dark under `data-theme="dark"`). Hosts the decorative blob, backdrop blur, and the content frame.
- **Decorative blob.** A 421×421 orange SVG positioned top-center (off-canvas, `top: -403px raw`), purely illustration. Recognition anchor for the AI moment.
- **Backdrop blur.** A full-bleed layer with `backdrop-filter: blur(100px)` and a 4%-white tint. Softens the blob into the sheet.
- **Content frame.** Absolutely positioned (`left: var(--ct-spacing-16)`, `top: 143px raw`, width 361px raw, gap `--ct-spacing-32`). Two slots: headline + AI notification card.
  - **Headline.** Simula H1-serif (32px), 2 lines, cream — the Kit voice moment. Editorial, not a screen title.
  - **AI notification card.** Fixed-dark `--ct-bkgd-ai-input` pill with 20px radius. Two slots: leading 40×40 guard avatar (with embedded autoplay video, `mix-blend: lighten`) + a stacked text column (252px raw) with primary recommendation (body, opacity 0.7 raw) over secondary tagline (body, text-secondary).

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `default` | 393×852 dark hero, decorative orange blob (off-canvas, blurred) over `--ct-bkgd-02` sheet, Simula H1 Kit headline + dark AI notification card with guard avatar and 2-line recommendation | AI handoff after a user prompt — Kit acknowledges input ("Got it…") and surfaces one recommended action |

**Sizing.**
- Container: width 393px (raw — no matching `--ct-spacing-*`); height 852px (raw — full mobile face); `position: relative`; `overflow: clip`. Background `--ct-bkgd-ai-input`.
- Components sheet: full bleed (393×852 raw); `position: sticky`; `top: 0`; `overflow: clip`. Background `--ct-bkgd-02` (dark theme).
- Orange blob: position absolute; centered horizontally (`left: 50%; transform: translateX(-50%)`); `top: -403px raw`; `width: 421px raw`; `height: 421px raw`. Inner SVG insets by `-14.25%` raw on all sides. Illustration — do not tokenize.
- Backdrop blur layer: position absolute; full bleed (393×852 raw); `backdrop-filter: blur(100px)` (raw — illustration); background `rgba(255, 255, 255, 0.04)` (raw — illustration; do not tokenize).
- Content frame: position absolute; `left: var(--ct-spacing-16)`; `top: 143px raw`; width 361px raw; `flex-direction: column`; `align-items: flex-start`; gap `--ct-spacing-32`.
  - Headline: width 348px raw; 2 lines; `line-height: 1` (matches `--ct-text-h1-serif-line-height`).
  - AI notification card: full width (361px raw); `flex-direction: row`; `align-items: center`; gap `--ct-spacing-20`; padding-inline `--ct-spacing-24`; padding-block `--ct-spacing-20`; border-radius `--ct-spacing-20` (= 20px, doubles as full pill at this height).
    - Guard avatar: `--ct-spacing-40` × `--ct-spacing-40` (40×40); SVG asset wraps an embedded autoplay video at `inset: 7px raw / 17.5% raw` with `mix-blend-mode: lighten` (raw — illustration). Geometry baked in the asset; do not redraw.
    - Text column: width 252px raw; `flex-direction: column`; `align-items: flex-start`. Primary label opacity `0.7` raw; secondary label full opacity.

**Tokens.**

| Slot | Property | Token |
| --- | --- | --- |
| Container | background | `--ct-bkgd-ai-input` |
| Components sheet | background | `--ct-bkgd-02` (resolves dark under `data-theme="dark"` — see note) |
| Orange blob | spec | _TBD_ — raw SVG illustration; do not tokenize |
| Backdrop blur | filter | `blur(100px)` (raw — illustration) |
| Backdrop blur | background | `rgba(255, 255, 255, 0.04)` (raw — illustration; no `--ct-bkgd-*` matches) |
| Content frame | left | `--ct-spacing-16` |
| Content frame | gap | `--ct-spacing-32` |
| Headline | color | `--ct-text-primary` (resolves cream under `data-theme="dark"`) |
| Headline | font (apply all 5) | `--ct-text-h1-serif-*` |
| AI notification card | background | `--ct-bkgd-ai-input` |
| AI notification card | padding-inline | `--ct-spacing-24` |
| AI notification card | padding-block | `--ct-spacing-20` |
| AI notification card | gap | `--ct-spacing-20` |
| AI notification card | border-radius | `--ct-spacing-20` |
| Guard avatar | size | `--ct-spacing-40` |
| Guard avatar | spec | _TBD_ — SVG asset bakes the avatar fill + animated overlay (same caveat as Component 1 §icon strokes — Figma must export the fill as a variable for theme-aware re-color) |
| Avatar video overlay | mix-blend-mode | `lighten` (raw — illustration) |
| Primary label | color | `--ct-text-primary` (resolves cream under `data-theme="dark"`) |
| Primary label | opacity | `0.7` (raw — only `--ct-opacity-disabled` = 0.3 exists; no match) |
| Primary label | font (apply all 5) | `--ct-text-body-*` |
| Secondary label | color | `--ct-text-secondary` |
| Secondary label | font (apply all 5) | `--ct-text-body-*` |

> _The Components sheet uses `--ct-bkgd-02`, which flips with theme. Under `data-theme="light"` it resolves to white and the dark-mode aesthetic (orange blob bloom, cream Simula, fixed-dark notification) breaks. The hero must be wrapped in `data-theme="dark"` so `--ct-bkgd-02`, `--ct-text-primary`, and `--ct-text-secondary` resolve to their dark-theme values. The outer floor (`--ct-bkgd-ai-input`) and the inner notification card both use AI tokens, which are pinned dark per SKILL.md §5.2 and do not flip._

**Don't.**
- Don't use Simula on the AI notification labels — Simula is scoped to the Kit headline only in this hero, even though §14 is one of the few components where Simula is sanctioned. One Simula moment per hero (SKILL.md §6.4).
- Don't extend the Simula headline to a third or fourth slot "to match the editorial voice." Adding a second Simula moment kills the contrast it exists to create (SKILL.md §6.4).
- Don't render this hero under `data-theme="light"` and hard-code dark hex values to compensate. The hero must sit in `data-theme="dark"` so `--ct-bkgd-02` and `--ct-text-*` flip naturally (SKILL.md §5.1, §5.4).
- Don't tokenize the backdrop-blur tint (`rgba(255, 255, 255, 0.04)`) as `--ct-color-white-05` or any `--ct-bkgd-*` token. It's a raw illustration value tuned against the orange blob behind it — see SKILL.md §2.1 / §4.4.
- Don't replace the guard avatar with a generic icon (e.g. `bell`, `info`, `chat`). The animated guard is the AI's visual signature and the recognition anchor for the Kit moment (SKILL.md §9.5).
- Don't replace the decorative orange blob with a flat color, a generic gradient, or `--ct-brand` painted across the sheet. The blurred orange blob *is* the Kit moment's visual signature — any substitution generic-ifies the hero (SKILL.md §9.5).
- Don't apply `--ct-text-ai-*` to the headline or the notification labels. This hero uses `--ct-text-primary` / `--ct-text-secondary` flipped via `data-theme="dark"`, not AI text tokens (SKILL.md §5.2).

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17826-13504) · Specimen frame `17826:13504` · Variant master: Kit Briefing `16196:2888`

### 15. Hero / Notification

**Use.** Standalone AI notification moment — a single fixed-dark notification card from Kit (AI persona) presented on the app's light cream surface, without the editorial headline of §14. Reach for it as a celebratory milestone or one-line status update from the AI when no Kit voice headline is appropriate.

**Anatomy.**
```
                cream surface
                ┌─────────────────────────────────┐
                │                                 │
                │  ╭───────────────────────────╮  │
                │  │ ◉  One Year Wrap          │  │   ← AI notification card (fixed-dark)
                │  │    From 25 to 64.         │  │      avatar (40×40, celebration) +
                │  │    Untouchable            │  │      2-line text column
                │  ╰───────────────────────────╯  │
                │                                 │
                └─────────────────────────────────┘
```
- **Outer surface.** A cream sheet on the app's light theme (`--ct-bkgd-01`). The card is the only content — no headline, no decorative blob, no backdrop blur (contrast with §14).
- **AI notification card.** Fixed-dark `--ct-bkgd-ai-input` pill with 20px radius. Two slots: leading 40×40 celebration avatar + a stacked text column (252px raw) with primary label (body, opacity 0.7 raw) over secondary tagline (body, text-secondary).
  - **Celebration avatar.** A green circular fill (`--ct-status-success-solid`, baked in the SVG asset) overlaid with a numeric glyph (e.g. "1") indicating the milestone. Distinct from the §14 Guard avatar — different recognition anchor for the celebration moment.

**Variants.**

| Variant | Visual | When |
| --- | --- | --- |
| `default` | 361px-wide fixed-dark AI notification card with celebration avatar (green + numeric glyph) and 2-line label stack, floating on a cream `--ct-bkgd-01` surface | Milestone celebration or one-line AI status update when no Simula headline is appropriate |

**Sizing.**
- Card: width 361px (raw — no matching `--ct-spacing-*`); `flex-direction: row`; `align-items: center`; gap `--ct-spacing-20`; padding-inline `--ct-spacing-24`; padding-block `--ct-spacing-20`; border-radius `--ct-spacing-20` (= 20px, doubles as full pill at this height).
  - Celebration avatar: `--ct-spacing-40` × `--ct-spacing-40` (40×40); SVG asset bakes the green ellipse fill and the numeric glyph (positioned at `left: 16px raw`, `top: 12px raw`, size 9×16 raw inside the 40×40 frame). Geometry baked in the asset; do not redraw.
  - Text column: width 252px raw; `flex-direction: column`; `align-items: flex-start`. Primary label opacity `0.7` raw; secondary label full opacity.

**Tokens.**

| Slot | Property | Token |
| --- | --- | --- |
| Outer surface | background | `--ct-bkgd-01` |
| AI notification card | background | `--ct-bkgd-ai-input` |
| AI notification card | padding-inline | `--ct-spacing-24` |
| AI notification card | padding-block | `--ct-spacing-20` |
| AI notification card | gap | `--ct-spacing-20` |
| AI notification card | border-radius | `--ct-spacing-20` |
| Celebration avatar | size | `--ct-spacing-40` |
| Celebration avatar | spec | _TBD_ — SVG asset bakes the green ellipse fill (visually `--ct-status-success-solid`) and the numeric glyph (same caveat as §1 icon strokes and §14 Guard avatar — Figma must export the fill as a variable for theme-aware re-color) |
| Primary label | color | `--ct-text-primary` (resolves cream when the card is wrapped in local `data-theme="dark"` — see note) |
| Primary label | opacity | `0.7` (raw — only `--ct-opacity-disabled` = 0.3 exists; no match) |
| Primary label | font (apply all 5) | `--ct-text-body-*` |
| Secondary label | color | `--ct-text-secondary` |
| Secondary label | font (apply all 5) | `--ct-text-body-*` |

> _Unlike §14 Hero / Kit Briefing — where the whole hero sits in `data-theme="dark"` so its `--ct-bkgd-02` sheet flips dark — this hero's outer surface is cream (`--ct-bkgd-01`) and must remain on `data-theme="light"`. The fixed-dark notification card therefore needs a local `data-theme="dark"` wrapper around the card itself so its `--ct-text-primary` and `--ct-text-secondary` resolve cream over the fixed-dark fill, while the surrounding cream surface stays unchanged. The card background (`--ct-bkgd-ai-input`) is pinned dark per SKILL.md §5.2 and does not flip._

**Don't.**
- Don't add a Simula headline above the card "to match §14." The absence of a headline is the whole point of this variant — it's the no-headline sibling. If a headline is needed, reach for §14 Hero / Kit Briefing instead (SKILL.md §6.4, §7.1).
- Don't apply `--ct-text-ai-*` to either label. Figma exports `--ct-text-primary` / `--ct-text-secondary` here (mirroring §14); the cream resolution comes from wrapping the card in local `data-theme="dark"`, not from the AI text family (SKILL.md §5.2).
- Don't render the card directly on a `data-theme="light"` surface without a local `data-theme="dark"` wrapper. Without it, `--ct-text-primary` resolves near-black on the fixed-dark card and the labels disappear (SKILL.md §5.1, §5.4).
- Don't repaint the celebration avatar's green circle by binding `--ct-status-success-solid` to a CSS fill. The fill is baked into the SVG asset; theme-aware re-color requires re-export from Figma (same caveat as §1 icon strokes and §14 Guard avatar — SKILL.md §2.1).
- Don't replace the celebration avatar with a generic icon (e.g. `bell`, `info`, `confetti`, `check`) or with the §14 Guard avatar. The green-circle-plus-numeric-glyph is this notification's visual signature; swapping it generic-ifies the moment and breaks the recognition contract with §14 (SKILL.md §9.5).

**Figma.** [Playlist — Toolkit](https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=16978-11906) · Specimen frame `16978:11906` · Variant master: ai-notification `16081:12390`

---
