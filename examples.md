# Examples

> Bridge between the design system and real screens.
> **What this file does**: shows how the main navigation tabs are assembled — how cards stack, how groups end, and how each feature's hero evolves across states.
> **What this file does NOT do**:
> - Define components → see `.claude/skills/cloaked-design-system/components.md`
> - List token values → see `tokens/colors.css`, `tokens/numbers.css`, `tokens/themes.css`, `tokens/typography.css`
> - State design rules → see `.claude/skills/cloaked-design-system/SKILL.md` §2.1

If you're about to add a token or define a component here, stop. You're in the wrong file.

---

## How to use this file

When designing or coding a new screen for Cloaked:

1. **Identify the section** — Home / Activities / Monitoring / Guard / Identity, or new.
2. **Identify the state** — day 1 (sparse), activated (just made first item), or 1 year (dense, accumulated)?
3. **Find the closest example below.** Use its **Composition** as your starting skeleton — including stack groupings and section footers.
4. **Open the Figma node via MCP** (URL is in each block). Verify component names, spacing, and token usage before writing code.
5. **Read the Decisions section.** Apply the bans ("do not...") strictly.
6. **Stop and ask** if you need a component or token that doesn't exist in `components.md` / `tokens/*.css`.

---

## Cloaked's main navigation tabs

These are the screens reached from the bottom navigation. They are the **spine** of the product.

| Tab | What it does |
|-----|--------------|
| **Home** | Dashboard. Surfaces score, summary of all features, recent activity. |
| **Activities** | Every security action Cloaked takes — removals, scans, blocks. |
| **Monitoring** | Two sub-screens behind one tab: **VPN** (location/connection) and **Data Removal** (broker scrubbing progress). Switched via tabs. |
| **Guard** | Spam management. Blocks suspicious calls, SMS, email. |
| **Identity** | Fake identity layer. Phone numbers, emails, cards, passwords, accounts that hide my real info online. |

---

## States

Most features have three possible states. Not every feature uses all three.

- **day 1** — feature exists but has no data yet. Hero shows a promise + single CTA.
- **activated** — user has made the first item (one phone number, one identity, etc.). Hero is unchanged from day 1, but a single ListItem appears below. Bridge state between day 1 and 1 year.
- **1 year** — data has accumulated. Hero transforms into proof (numbers, charts, maps). Multiple stacks with section footers.

Currently in this file:
- **Home**: 1 year
- **Activities**: day 1, 1 year
- **Monitoring (VPN)**: day 1, 1 year
- **Monitoring (Data Removal)**: day 1, 1 year
- **Guard**: day 1, 1 year
- **Identity**: day 1, activated, 1 year

---

## Cross-cutting patterns

Rules that apply to **every** screen below. Do not restate these in individual examples.

1. **Hero evolution: day 1 → activated → 1 year**
   The hero module is the same slot, but its content transforms by state.
   - **Day 1**: hero = a **promise**. Placeholder visual + single CTA ("Get up Call Guard", "Secure my connection", "Get Started").
   - **Activated**: hero is **unchanged** from day 1. The change is below — one ListItem appears showing the just-created item.
   - **1 year**: hero = **proof**. Large number, chart, or map. Multiple data stacks below.
   - The hero **slot does not move or resize** between states. Only its content changes.

2. **Hero color = feature identity**
   Each feature owns a color/treatment that runs through hero, FAQ accents, and key surfaces.
   - Activities: orange · Monitoring: purple · Guard: gold/ochre · Identity: dark blue · Home: warm neutral

3. **Every page ends with one closing footer — `Footer / faq` OR `Footer / impact`, never both.**
   Pick one per page. `faq` is the fixed-dark AI band with the Section Header + horizontal carousel; `impact` is the cream editorial band with the inline Simula number + Tertiary CTA. The closer is positional, not stackable.

4. **Stack with section footers**
   Cards never just float. They are grouped into **stacks**, and most stacks end with a **section footer CTA**.
   - Group boundaries are visual (gap change, surface change), not just spacing.
   - Section footer CTA sits **inside** the group, at the bottom, before the next group starts.
   - Common footer patterns:
     - `"See all"` — link, navigates to full list
     - `"See more"` — link, expands inline
     - `"Add to dashboard"` — button, primary action
     - `"Explore tools"` — button on a social proof block
   - If a stack has nothing to navigate to, **no footer**. Don't invent one.

5. **Empty states are explicit**
   Day 1 always names what's coming: "Activity history will show here." Never leave a blank area.

6. **Hero number = headline**
   On 1 year states, the largest type on the page is the count, not the section title.

7. **Reuse, don't reinvent**
   If `List Item` (or any component) can carry the data, use it. Do not build "activity row", "scan row", "session row".

8. **Tabs inside a feature are navigational**
   When a single feature has multiple sub-screens (e.g. Monitoring → VPN / Data Removal / Dark Web), use tabs at the top — these are navigation, not filters. Use Segmented Control only when filtering one list (e.g. Identity's All / Phone / Email / Card / Password / Account).

---

## Reading the Composition format

Each example's Composition shows the **stack** top to bottom. Stack groups are boxed, section footers are marked.

```
1. [Component]                          ← full-bleed / standalone
2. ┌─ Group: [group name] ─────────────
   │  - [Component]
   │  - [Component]
   │  └ footer CTA: [type, label]
3. ┌─ Group: [group name] ─────────────
   │  - [Component] × n
   │  └ footer CTA: "See all" (link)
4. [Component]                          ← FAQ Section, etc.
```

This format makes three things visible at once: **what's stacked**, **where groups break**, and **what closes each group**.

---

## Examples

Each example follows the same four-part structure:
**Composition (stack)** → **Tokens** → **Decisions** → **Refs**.

States of the same feature are placed **together** so the evolution is visible.

---

### Home — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17492-12966&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/home`                              ← "Profile" right-aligned, no title
2. Hero / Kit Briefing                                     ← full-bleed; Simula H1 + AI notification card slot
3. ┌─ Group: Dashboard ──────────────────────────────────
   │  inline header: "Dashboard" + "Edit" (right)
   │  - Card / Dashboard  `list/digital-risk`              (Digital risk · High + exposure bar)
   │  - Card / Dashboard  `list/actions-taken`             (4,216 + ↑ 4 Today + 3 stat rows)
   │  - Card / Dashboard  `list/recent-activity`           (In Progress / Up Next bands + 3 progress rows)
   │  └ footer CTA: Button `text/secondary`, "Add to dashboard"
4. Footer / `faq`                                          ← horizontal scroll, 5 Simula H2 cards
```

**Tokens**
- Hero floor: `--ct-bkgd-ai-input` (fixed-dark). Hero sheet: `--ct-bkgd-02` resolved dark via local `data-theme="dark"`. Headline: `--ct-text-h1-serif-*` (Simula 32, cream).
- Dashboard panel surface: `--ct-bkgd-01` (cream). Tiles: `--ct-bkgd-02` (white under light theme). Tile-to-tile gap inside the panel: 24px (raw — `--ct-spacing-24` matches but this is panel-internal layout, not the cross-cutting section gap).
- KPI number "4,216": `--ct-text-display-2-*` (sans, 48px — Simula stays out of numbers per components.md §12).
- Stat pill "4 Today": defers to Label §3 `stat/up` — `--ct-status-success-subtle` container, `--ct-status-success-solid` text.
- FAQ band: `--ct-bkgd-ai-input` (fixed-dark, AI band). Question headlines: `--ct-text-h2-serif-*` (Simula 24). Accent label ("1 yr since you joined", "Score", "Goal", "Urgency", "Trusting Family"): `--ct-brand` (#ff550c).
- Section padding around the FAQ tail: `--ct-spacing-240` bottom (matches the Hero / Kit Briefing footprint per components.md §14).

**Decisions**
- **Home 1-year hero is Hero / Kit Briefing, not a feature hero.** Home keeps Kit's editorial briefing at the top because it summarizes every feature. The proof appears in the Dashboard group (`list/digital-risk`, `list/actions-taken`, `list/recent-activity`) rather than in a single feature-specific hero.
- **The orange blob in Kit Briefing is illustration, not feature identity.** Per components.md §14 it's the AI-moment recognition anchor. Don't read it as a Home feature color.
- **Dashboard tiles are `list/*` variants, never `kpi/*`.** Each composite tile (`list/digital-risk`, `list/actions-taken`, `list/recent-activity`) owns its own `card-section` footer ("See Details" / "See all activities") — those are component-internal per components.md §12, not stack-level group footers.
- **Group footer = "Add to dashboard" Button (Secondary).** This is the only stack-level footer for the Dashboard group, sitting inside the cream panel before the FAQ band.
- **FAQ accent = `--ct-brand`.** Home has no feature color (cross-cutting #2 → warm neutral), so its FAQ accent inherits the brand. Don't introduce a Home-only accent token.
- **Inline "Dashboard / Edit" panel header is one-off, not Section Header §7.** Body 16px on `--ct-bkgd-01` cream; §7 spec is H3 20px on `--ct-bkgd-02`. Code it inline here — do not promote to a Section Header variant.

**Refs**: → `components.md`

### Activities — day 1

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17492-12607&m=dev

**Composition (stack)**
```
1. Hero / Feature  `scanning/data-removal`             ← full-bleed; counter video + "Places data is exposed" + footer Status pill
   ⤷ Navigation  `top_bar/page`                        ← overlaid; title "Activities" only, no trailing
2. ┌─ Group: In Progress ─────────────────────────────
   │  Section Header  `default`                        ("In Progress")
   │  - List Item  `progress`                          (Removing you from Spoeko · Day 2 of 3)
   │  - List Item  `progress`                          (Monitoring 4 new breach alerts · Scanning now)
3. ┌─ Group: Next Steps ──────────────────────────────
   │  Section Header  `default`                        ("Next Steps")
   │  - List Item  `progress`                          (Preparing removal request for Whitepages · Start on Jan 13)
4. ┌─ Group: Today ───────────────────────────────────
   │  Section Header  `default`                        ("Today")
   │  - List Item  `empty`                             ("Activity History will show here")
5. Footer / `impact`                                   ← cream band; Simula brand "170 million" + Tertiary "Explore tools"
```

**Tokens**
- Hero surface: raw `#000` (per components.md §13 — no `--ct-bkgd-*` resolves to pure black; TBD). Orange overlay: `--ct-brand` with `mix-blend-mode: multiply`. Wrapped in `data-theme="dark"` so caption + status text resolve cream.
- Counter video & footer Status pill: video raw illustration; pill defers to Label §3 `status/active`.
- Navigation overlaid: Simula H2 (`--ct-text-h2-serif-*`), text `--ct-text-primary` (cream via inherited `data-theme="dark"`).
- Section Header `default`: surface `--ct-bkgd-02`, title `--ct-text-h3-*` capitalize, padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`.
- List Item `progress`: surface `--ct-bkgd-02`, padding `--ct-spacing-20`, gap `--ct-spacing-12`, leading 40×40 `Default_monitoring/Data Removal` avatar, title `--ct-text-body-*` + meta `--ct-text-body-small-*` `--ct-text-secondary`, bottom hairline `--ct-divider`. Progress bar 8px raw; track `--ct-bkgd-01`.
  - **Progress fill on this screen = `--ct-status-success-solid`** (deviates from List Item §6 spec, which mandates `--ct-brand` — see Decisions).
- List Item `empty`: surface `--ct-bkgd-02`, height 240px raw, copy `--ct-text-body-*` `--ct-text-primary`, centered.
- Footer / `impact`: surface `--ct-bkgd-01`, height 550px raw, inner stack 271px raw centered. Copy at `--ct-text-h3-*` capitalize; inline Simula on "170 million" via `--ct-text-h2-serif-*` colored `--ct-brand`. CTA pill `--ct-cta-secondary-container`, label `--ct-text-body-*`.

**Decisions**
- **Hero is `scanning/data-removal`, not a static-number hero.** No Display-1 number on this screen — the live counter video is the visualization, captioned by "Places data is exposed". The orange identity comes from `--ct-brand` mix-blend-multiply over a black surface, not a feature gradient.
- **Two active sections render on day 1: In Progress + Next Steps.** Cloaked is already running scans before any history exists; the empty state is scoped to the *Today* (history) section only — not the whole screen.
- **Progress-bar fill on Activities = `--ct-status-success-solid` (green).** Activities-specific override of the List Item §6 default (`--ct-brand`). Treat as intentional — live scanning reads as success — and don't unify across screens.
- **Activities closes with `Footer / impact`, not `Footer / faq`.** Per cross-cutting #3 a page picks one closer; here the editorial moment ("170 million records") is the close.

**Refs**: → `components.md`

### Activities — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17492-12608&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Activities"
2. Hero / KPI region                                   ← custom for Activities — see Decisions
   ⤷ kicker "Actions taken to protect you" (body-small)
   ⤷ Display-2 number "4,216" + Stat `stat/up` "4 Today"
   ⤷ 3-tile horizontal breakout: Card / Feature `default` (activity), category-tinted ×3
        · Monitoring · 342 · "Data removed"
        · Guard      · 234 · "Spam blocked"
        · Identity   ·  13 · "Identities created"
   ⤷ caption row: "Since · Feb 06.2026"
3. ┌─ Group: In Progress ─────────────────────────────
   │  Section Header  `default`
   │  - List Item  `progress` ×2                       (Removing you from Spoeko · Day 2 of 3 / Monitoring 4 new breach alerts · Scanning now)
4. ┌─ Group: Next steps ──────────────────────────────
   │  Section Header  `default`
   │  - List Item  `progress` ×1                       (Preparing removal request for Whitepages · Start on Jan 13 — no fill bar yet)
5. ┌─ Group: Scan history ────────────────────────────
   │  Section Header  `dropdown`                       (title "Scan history" + Control `dropdown/collapsed` "Latest")
   │  Divider time-bands + List Item ×8                (interleaved by date — "10 mins ago", "1 hr ago", "2:30pm", "Jan 15, 2026" ×2, "Jan 14, 2026"; rows mix progress / event / contact / List Item_VPN variants)
   │  └ footer CTA: Footer `card-section`, "See more"
6. Footer / `impact`                                   ← cream band; Simula brand "170 million" + Tertiary "Explore tools"
```

**Tokens**
- Hero KPI block: surface `--ct-bkgd-02`. Kicker `--ct-text-body-small-*` `--ct-text-primary`. Number `--ct-text-display-2-*`. Stat pill defers to Label §3 `stat/up` (`--ct-status-success-subtle` container, `--ct-status-success-solid` text).
- 3-tile breakout (Card / Feature `default`, category-tinted): tile surfaces `--ct-monitoring-container-02` (#5936c1), `--ct-guard-container-02` (#d78e20), `--ct-identity-container-02` (#379aad). Number `--ct-text-display-2-*`, label `--ct-text-body-small-*`. Tile text resolves cream via local `data-theme="dark"` (the category container is fixed-dark per Card / Feature §11 / SKILL.md §9.1).
- "Since" caption: `--ct-text-body-small-*` `--ct-text-secondary`.
- Section Header `default` and `dropdown`: surface `--ct-bkgd-02`, title `--ct-text-h3-*` capitalize, padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`. Dropdown chip defers to Control §5 `dropdown/collapsed`.
- List Item `progress` (Activities rule): surface `--ct-bkgd-02`, padding `--ct-spacing-20`, gap `--ct-spacing-12`, leading 40×40 `Default_monitoring/Data Removal`, title `--ct-text-body-*` + meta `--ct-text-body-small-*` `--ct-text-secondary`, bottom hairline `--ct-divider`. Progress bar 8px raw, track `--ct-bkgd-01`, **fill `--ct-status-success-solid`** (Activities-screen rule, see Decisions).
- Time-band Divider rows: defer to Divider §2 (cream band, `--ct-bkgd-01`, body-small label).
- Footer `card-section`: top hairline `--ct-divider`, link `--ct-text-link-*` `--ct-text-primary`, height 50px raw.
- Footer / `impact`: same tokens as Activities — day 1 (cream `--ct-bkgd-01` band, inline Simula `--ct-brand` "170 million", Tertiary CTA).

**Decisions**
- **The hero region is not a Hero / Feature §13 variant.** Composition (kicker + Display-2 + Stat + 3-tile breakout + "Since" caption) does not match any of the 7 closed `intro/* | active/* | scanning/*` variants. Treat as a custom Activities-1-year hero pattern; flag if a new `active/activities` variant should be added to §13.
- **The 3 breakout tiles tint Card / Feature `default` (activity) with category tokens.** Per Card / Feature §11 Don't #1, only the `automation` variant may consume `--ct-monitoring-*` / `--ct-guard-*` / `--ct-identity-*`; tinting Activity tiles is explicitly forbidden. The Figma master uses them here anyway. _Question for the user: is this an intentional Activities-page exception (the breakout surfaces other features' results, so feature colors carry meaning), or should the tiles switch to white `default` (activity) surfaces to comply with §11?_
- **Activities — 1 year hero shows other features' identity colors, not its own brand orange.** Activities is the meta-feature that summarizes what Monitoring / Guard / Identity did, so the breakout uses their colors. Brand orange (the Activities identity per cross-cutting #2) does not appear in the hero — it stays scoped to the day-1 `scanning/data-removal` hero and to the Footer / impact's "170 million".
- **Progress-bar fill = `--ct-status-success-solid` (green) here too.** Activities-screen rule (see day 1). Don't unify with `--ct-brand` from List Item §6.
- **Scan history is a single composite stack — not a card group.** Section Header `dropdown` (filterable by "Latest") + mixed List Item variants (progress / event / contact / VPN) interleaved with date-band Dividers + `card-section` "See more" footer. Date Dividers sit between rows, not at group boundaries.
- **Closes with `Footer / impact`, same as day 1.** No FAQ band (cross-cutting #3).

**Refs**: → `components.md`

---

### Monitoring (VPN) — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero is the empty map + "Secure my connection" CTA._
- _Tabs (VPN / Data Removal / Dark Web Monitoring) at top — VPN is selected._
- _Why purple._

**Refs**: → `components.md`

### Monitoring (VPN) — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Map fills with location dots. "Connected" status row appears with timer + Disconnect button._
- _New stacks: Locations group, Total Average stat trio (Locations / Hours / Data used), Recent Session list with time grouping ("Today" / "Yesterday")._

**Refs**: → `components.md`

---

### Monitoring (Data Removal) — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Different from VPN day 1 — Data Removal leads with a Progress checklist (scan complete / removal request sent / waiting for response / broker response / removal confirmed)._
- _Same purple identity as VPN. Same tabs at top._

**Refs**: → `components.md`

### Monitoring (Data Removal) — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero shows "Total Removed 276" + next scan date + bar chart over time._
- _New stacks: What Was Found list (Phone / Name / Family / Address / Email with site counts), Automation Packs ("Remove From Major Brokers" with brand logos), Scan History with progress per broker._

**Refs**: → `components.md`

---

### Guard — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero shows a sculpted illustration + "Block Suspicious Calls In Real Time" headline + "Get up Call Guard" CTA + "Set up · 2 minutes" meta._
- _Tabs (Call Guard / SMS Guard / Email Guard) at top._
- _Why gold/ochre._

**Refs**: → `components.md`

### Guard — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero becomes "Calls Blocked 324" + week heatmap with Week/Month/Year toggle._
- _New stack: Recent History group (Cloaked Support / Unknown call / Medical scam ListItems with Voicemail/Missed Call labels) with "See all" footer._

**Refs**: → `components.md`

---

### Identity — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero shows a silhouetted figure + "Never Give Away Your Real Information Again" headline + "Get Started" CTA + sample fake email "crayon@cloaked.id"._
- _Filter chips at top (All / Phone / Email / Card / Password / Account) — Segmented Control, not Tabs (filtering, not navigation)._
- _Why dark blue._

**Refs**: → `components.md`

### Identity — activated

> Bridge state. User has just created their first identity item.

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero is **unchanged** from day 1. The only change is below: one category section appears (e.g. "Phone Numbers") with one ListItem (e.g. "Doordash · Restaurant · 342-231-1234") + "+ Create new number" button._
- _All other categories (Email / Card / Password / Account) are still hidden — only the activated category is shown._

**Refs**: → `components.md`

### Identity — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero is gone — replaced by the full category list. No hero number; Identity is list-dominant._
- _All 5 categories appear, each with the same group structure: Section Header → ListItems → "+ Create new {category}" button → "See all" link._

**Refs**: → `components.md`

---

## Sub-screens

The 12 blocks above cover the main nav tabs and key states. Sub-screens (drill-downs from these tabs) are not listed individually — they inherit their parent feature's identity and follow the same patterns.

If a sub-screen breaks a pattern from above, that's a signal to **discuss before designing**, not to extend this file.

---

## Decision tree — which example should I look at?

| If you're building... | Look at |
|-----------------------|---------|
| A dashboard summarizing multiple features | Home — 1 year |
| A new feature's empty/onboarding state | Any "— day 1" block, closest in data type |
| A bridge state with first item created | Identity — activated |
| A feature's data-rich state with progress/scans | Activities — 1 year |
| A feature with map + connection state | Monitoring (VPN) — 1 year |
| A feature with progress checklist | Monitoring (Data Removal) — day 1 |
| A feature with broker/automation grid | Monitoring (Data Removal) — 1 year |
| A feature centered on a single metric + heatmap | Guard — 1 year |
| A list-dominant feature with repeating categories | Identity — 1 year |
| Anything else | Find the closest above, then ask before deviating |

---

## Maintenance

- **Source of truth is Figma.** When the Figma file changes, update this file.
- **Component names must match Figma component names exactly** — this file is read by AI tools via Figma MCP.
- **The 12-block scope is intentional.** These are the main nav tabs and key states. Adding sub-screens here will dilute the patterns.
- **If you'd add a new block, ask first** whether it's a new pattern or an instance of an existing one.
