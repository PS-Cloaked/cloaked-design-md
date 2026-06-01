# Examples

> Bridge between the design system and real screens.
> **What this file does**: shows how the main navigation tabs are assembled — how cards stack, how groups end, and how each feature's hero evolves across states.
> **What this file does NOT do**:
> - Define components → see `components.md`
> - List token values → see `tokens/colors.css`, `tokens/numbers.css`, `tokens/themes.css`, `tokens/typography.css`
> - State design rules → see `SKILL.md` §2.1

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
- **Inline "Dashboard / Edit" panel header is one-off, not Section Header §7.** Body 16px on `--ct-bkgd-01` cream; §7 spec is H4 20px on `--ct-bkgd-02`. Code it inline here — do not promote to a Section Header variant.

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
- Section Header `default`: surface `--ct-bkgd-02`, title `--ct-text-h4-*` capitalize, padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`.
- List Item `progress`: surface `--ct-bkgd-02`, padding `--ct-spacing-20`, gap `--ct-spacing-12`, leading 40×40 `Default_monitoring/Data Removal` avatar, title `--ct-text-body-*` + meta `--ct-text-body-small-*` `--ct-text-secondary`, bottom hairline `--ct-divider`. Progress bar 8px raw; track `--ct-bkgd-01`.
  - **Progress fill on this screen = `--ct-status-success-solid`** (deviates from List Item §6 spec, which mandates `--ct-brand` — see Decisions).
- List Item `empty`: surface `--ct-bkgd-02`, height 240px raw, copy `--ct-text-body-*` `--ct-text-primary`, centered.
- Footer / `impact`: surface `--ct-bkgd-01`, height 550px raw, inner stack 271px raw centered. Copy at `--ct-text-h4-*` capitalize; inline Simula on "170 million" via `--ct-text-h2-serif-*` colored `--ct-brand`. CTA pill `--ct-cta-secondary-container`, label `--ct-text-body-*`.

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
- 3-tile breakout (Card / Feature `default`, category-tinted): tile surfaces `--ct-monitoring-container-02` (#291132), `--ct-guard-container-02` (#5B3B0D), `--ct-identity-container-02` (#0E1F31). Number `--ct-text-display-2-*`, label `--ct-text-body-small-*`. Tile text resolves cream via local `data-theme="dark"` (the category container is fixed-dark per Card / Feature §11 / SKILL.md §9.1).
- "Since" caption: `--ct-text-body-small-*` `--ct-text-secondary`.
- Section Header `default` and `dropdown`: surface `--ct-bkgd-02`, title `--ct-text-h4-*` capitalize, padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`. Dropdown chip defers to Control §5 `dropdown/collapsed`.
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

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17492-13488&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Safety Monitoring"
2. Tabs (sticky, undocumented — see Decisions)         ← VPN (selected) / Data Removal / Dark Web Monitoring
3. Hero / Feature  `intro/vpn`                         ← cream surface + dotted world map + top-right ButtonIconPrimary expand + H1 title "Your Internet, / But More Private" + Primary CTA "Secure my connection"
4. Footer / `faq`  (feature-tinted)                    ← 4 cards; band tinted with `--ct-monitoring-container-02`, cards `--ct-monitoring-container-01` (see Decisions)
```

**Tokens**
- Navigation `top_bar/page`: title "Safety Monitoring", `--ct-text-h2-serif-*` (Simula 24), `--ct-text-primary` (resolves dark on the cream `--ct-bkgd-01` outer surface).
- Tabs: backdrop-blur 16px raw, bottom border `--ct-divider`, padding-top `--ct-spacing-48`, padding-inline `--ct-spacing-16`, gap 10px raw. Each Tap_item: `--ct-text-body-*` `--ct-text-primary`, padding-block `--ct-spacing-20`. Selected: bottom-border `--ct-cta-primary-container`. Inactive: `opacity: var(--ct-opacity-disabled)` (0.3).
- Hero `intro/vpn` (defers to Hero / Feature §13): container `--ct-bkgd-01`. Top-right Button defers to `icon-primary/default`. Title `--ct-text-h1-*` capitalize `--ct-text-primary`. CTA: container `--ct-monitoring-container-02`, label `--ct-cta-primary-text`.
- Footer / `faq` (feature-tinted): container `--ct-monitoring-container-02` (#291132). FAQ cards: surface `--ct-monitoring-container-01` (#411d50). Section title "Frequently Asked Questions": `--ct-text-h4-*` capitalize, `--ct-text-primary` cream via local `data-theme="dark"`. FAQ card kicker: `--ct-text-body-small-*` `--ct-text-ai-secondary` (#dcd8cf) — **not `--ct-brand`**. FAQ card headline: `--ct-text-h2-serif-*` `--ct-text-ai-primary`. Trailing icon button: `Button_Icon/Secondary` (48×48 round, `action/arrow_right`). Container padding-bottom `--ct-spacing-240`.

**Decisions**
- **Hero matches Hero / Feature §13 `intro/vpn` exactly.** The brand-purple Primary CTA (`--ct-monitoring-container-02`) is the visual signature of the VPN moment; per §13 it is the only sanctioned override of `--ct-cta-primary-container`. Cream surface + 11 dot markers on the world map + the expand `ButtonIconPrimary` are part of the variant — don't substitute a generic illustration.
- **Page title is "Safety Monitoring", not "Monitoring" or "VPN".** "Monitoring" is the internal feature/tab name; "Safety Monitoring" is the user-facing page title. The three tabs (VPN / Data Removal / Dark Web Monitoring) live below the title and switch sub-screens (cross-cutting #8 navigational tabs).
- **Tabs are an undocumented component.** Sticky horizontal strip, backdrop-blur 16px raw, three `Tap_item` rows; the selected tab carries a bottom border (`--ct-cta-primary-container`), inactive tabs use `--ct-opacity-disabled`. components.md has no Tabs spec yet — Control §5 covers Dropdown / Toggle but not this strip. _Question for the user: promote Tabs to a new component spec, or accept inline for now?_
- **FAQ band is feature-tinted, not the default fixed-dark AI band.** Container `--ct-monitoring-container-02`, cards `--ct-monitoring-container-01`, kickers `--ct-text-ai-secondary` (cream-grey) — NOT `--ct-brand`. This realizes cross-cutting #2 ("color runs through FAQ accents") but **contradicts components.md §9 Footer / faq Don't #8** ("Don't tint the FAQ card surface with `--ct-monitoring-*` / `--ct-guard-*` / `--ct-identity-*`"). _Question for the user: §9 needs a feature-tinted variant documented (or the Don't #8 rule revised) — flag for follow-up?_
- **No In Progress / Next Steps / history sections on VPN day 1.** The screen is pure: Nav → Tabs → Hero → FAQ. The hero is the day-1 promise; nothing else is needed before activation (cross-cutting #1).

**Refs**: → `components.md`

### Monitoring (VPN) — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17676-8649&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Safety Monitoring"
2. Tabs (sticky)                                       ← VPN selected / Data Removal / Dark Web Monitoring
3. Hero / Feature  `active/vpn`                        ← map + top-right ButtonIconPrimary; bottom detail card: Connected · 03:45:82 / Service · New York 🇺🇸 / Disconnect Primary CTA
4. ┌─ Group: Locations ──────────────────────────────
   │  Section Header  `default`
   │  - Card / Feature  `location` ×3                  (United States · Fastest / New York · Dedicated IP / Brazil · Fastest — horizontal row, 160px each)
5. ┌─ Group: Total Average ───────────────────────────
   │  Section Header  `default`
   │  Stat trio (undocumented — see Decisions): 12 · Locations | 124h · Hours | 332GB · Data used
6. ┌─ Group: Recent session ──────────────────────────
   │  Section Header  `dropdown`                       (title "Recent session" + Control `dropdown/collapsed` "All")
   │  Divider "Today"  + List Item_VPN ×2              (New York / JFK Airport · 2h 14m · 1.2GB · Seattle / SEA Airport · 1h 14m · 1.2GB)
   │  Divider "Yesterday" + List Item_VPN ×2           (Sao Paulo / GRU Airport · 2h 14m · 1.2GB · Hoboken / Starbucks Hoboken · 1h 14m · 1.2GB)
   │  └ footer CTA: Footer `card-section`, "See all"
7. Footer / `faq`  (feature-tinted)                    ← 4 cards; same monitoring tokens as VPN — day 1
```

**Tokens**
- Navigation, Tabs: same as Monitoring (VPN) — day 1.
- Hero `active/vpn` (defers to Hero / Feature §13): container `--ct-bkgd-01`. Map illustration raw. Top-right Button defers to `icon-primary/default`. Detail card surface `--ct-bkgd-02`, padding-inline `--ct-spacing-20`, padding-bottom `--ct-spacing-40`. Connected row + Service row body 16 `--ct-text-primary`; hairline `--ct-divider`. Flag avatar 40×40 raw illustration. Disconnect CTA defers to Button `text/primary` — uses **default `--ct-cta-primary-container`** (dark), NOT `--ct-monitoring-container-02` (see Decisions).
- Locations group: Section Header `default` (`--ct-bkgd-02`, H4 capitalize). Card / Feature `location` ×3: cream surface `--ct-bkgd-01`, padding `--ct-spacing-16`, gap `--ct-spacing-12`, radius `--ct-spacing-20`. Flag avatar 40×40. City: `--ct-text-body-*` `--ct-text-primary`. Descriptor at raw `opacity: 0.5` per §11.
- Total Average stat trio: surface `--ct-bkgd-02`, 353px raw row width. Number `--ct-text-h1-*` (32px, letter-spacing 0.5 — note: §13 active heroes use Display-1, but this stat trio uses H1, smaller). Label `--ct-text-link-*` (12px) `--ct-text-primary`. Two vertical dividers 72px raw, `--ct-divider`.
- Recent session: Section Header `dropdown` — Dropdown chip defers to Control §5 `dropdown/collapsed` (cream pill on `--ct-bkgd-01`, radius `--ct-spacing-24`). Date Dividers defer to Divider §2 (cream band, body-small label). List Item_VPN: surface `--ct-bkgd-02`, padding `--ct-spacing-20`. Leading 40×40 flag avatar. Title body `--ct-text-primary` + meta body-small `--ct-text-secondary`. Trailing 2-line text block per List Item §6 (duration body primary + data body-small secondary, right-aligned). Bottom hairline `--ct-divider`. Footer `card-section`: top hairline + body-link "See all".
- Footer / `faq` (feature-tinted): same monitoring tokens as VPN — day 1 (`--ct-monitoring-container-02` band, `--ct-monitoring-container-01` cards, `--ct-text-ai-secondary` kicker, `--ct-text-ai-primary` Simula H2 headline). 4 cards.

**Decisions**
- **Hero matches Hero / Feature §13 `active/vpn` exactly.** Per §13 the Disconnect CTA uses the default Button `text/primary` (`--ct-cta-primary-container` = near-black) — **NOT** `--ct-monitoring-container-02`. The monitoring-purple CTA is reserved for `intro/vpn` (the day-1 promise). Don't carry the purple over to the active state "for consistency."
- **VPN's hero has no Display-* hero number, in either state.** Cross-cutting #6 ("Hero number = headline") does not apply here — the proof on day-1 is the promise CTA, on 1-year it's the live connection state ("Connected · 03:45:82"). The 12 / 124h / 332GB counts live in the Total Average section, not the hero.
- **Locations row = Card / Feature `location` ×3 in a horizontal row.** Cream surfaces, 40×40 flag avatars, city + descriptor at raw 0.5 opacity (§11). The row is part of the stack — don't promote to a horizontal-scroll carousel; the 3 cards fit at 160px each on a 393px page.
- **"Total Average" stat trio is undocumented.** Three H1 (32px) numbers separated by two vertical 72px dividers, on a white card. Doesn't match Card / Dashboard `kpi/*` (which uses Display-2 + a visualization slot) or any Card / Feature variant. _Question for the user: promote to a new spec (e.g. Card / Stat-trio) or accept inline?_
- **Recent session = same composite pattern as Activities — 1 year Scan history.** Section Header `dropdown` + Divider date-band + List Item rows + `card-section` "See all" footer. Here the rows are the VPN-specific List Item_VPN variant (flag avatar + city/place + duration/data trailing).
- **FAQ band feature-tinted, same as VPN — day 1.** Continues the contradiction with components.md §9 Don't #8 — already flagged at VPN day 1; not re-flagged here.

**Refs**: → `components.md`

---

### Monitoring (Data Removal) — day 1

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17651-5310&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Safety Monitoring"
2. Tabs (sticky)                                       ← VPN / Data Removal (selected) / Dark Web Monitoring
   ⚠  No Hero on this screen — see Decisions
3. ┌─ Group: Progress ───────────────────────────────
   │  Section Header  `default`                        ("Progress")
   │  - Timeline  `completed-first`                    (Scan complete · 33 sites)
   │  - Timeline  `completed-middle`                   (Removal request sent)
   │  - Timeline  `current-middle`                     (Waiting for response · Typically 7-14 days)
   │  - Timeline  `upcoming-middle`                    (Broker response · 33 sites)
   │  - Timeline  `upcoming-last`                      (Removal confirmed)
4. ┌─ Group: what was found ──────────────────────────
   │  Section Header  `default`
   │  - Stat row ×5 with leading colored dot (see Decisions): Phone number · 19 sites / Name · 17 sites / Family members · 14 sites / Address · 13 sites / Email · 12 sites
5. ┌─ Group: Your Info ───────────────────────────────
   │  Section Header  `action`                         (title "Your Info" + "Edit")
   │  - Stat row ×4: Full Name · Lucas Weiner / Date of birth · 02/12/1998 / Phone · (212)555-0101 / Email · Lucas@cloaked.com
   │  └ footer CTA: Footer `card-section`, "See Details"
6. Footer / `faq`  (feature-tinted)                    ← 4 cards; same monitoring tokens
```

**Tokens**
- Navigation, Tabs: same as Monitoring (VPN) — day 1.
- Progress group: surface `--ct-bkgd-02`. Section Header `default`. Each row defers to Timeline §8 — shell + connector + title/meta. Completed shells `--ct-brand` (#ff550c) + check icon; current shell `--ct-graph-background` (rgba(11,11,10,0.05)) + timer + 40×40 halo overlay; upcoming shells `--ct-graph-background` + step-specific feature icon. Connectors: brand for past, graph-background for future, boundary at the bottom of the current step (per §8). Title `--ct-text-body-*` `--ct-text-primary`; meta `--ct-text-body-small-*` `--ct-text-secondary`.
- "what was found" stat rows: surface `--ct-bkgd-02`, row width 360px raw (NOT the §6 Stat's 322px), padding-block `--ct-spacing-24`, gap `--ct-spacing-8` between dot + label. Leading 6.286px raw colored dot (5 distinct hexes, illustration — see Decisions). Label width 146px raw, value width 160px raw, both `--ct-text-body-*` `--ct-text-primary`. Row hairline `--ct-divider`.
- "Your Info" stat rows: same shape as "what was found" minus the leading dot. Section Header `action` per §7 (title left, "Edit" plain text right, body sans, no container). Footer `card-section` "See Details" at the bottom.
- Footer / `faq` (feature-tinted): same monitoring tokens as VPN — day 1.

**Decisions**
- **No Hero / Feature on this screen.** Cross-cutting #1's "day 1 = hero promise + single CTA" does not apply to Data Removal — the user enters straight into the live Progress timeline. The Tabs strip is the only thing between the page title and the data. Don't insert a placeholder Hero "to fill the slot."
- **Progress is a Timeline §8 stack, not a List Item / progress stack.** Five steps in a fixed sequence (Scan complete → Removal request sent → Waiting for response → Broker response → Removal confirmed) with exactly one `current-middle` step at a time. Connector colors encode progression (brand for past, graph-bg for future) per §8. Don't use List Item `progress` rows here — those are for parallel scans / monitoring tasks; this is one linear path.
- **"what was found" rows are an undocumented stat-row shape.** Width 360px raw, padding-block `--ct-spacing-24`, leading 6.286px raw colored dot per category (5 distinct hexes — the same palette pattern as Hero / Feature §13 `active/data-removal` category bars, but rendered as dots, not bars). List Item §6 Stat is 322px / py-16 / no leading slot — close but different. _Question for the user: promote this to a List Item §6 variant (e.g. `stat/category-dot`), or accept inline?_
- **"Your Info" uses Section Header `action` for the Edit affordance** (per §7). The same row-shape as "what was found", minus the dot, plus a `card-section` "See Details" footer — that combination is the formula for the read-only edit-able profile group on this screen.
- **Tabs and FAQ band reuse the Monitoring identity** — purple feature color via `--ct-monitoring-container-02` / `_01` (FAQ tinting flagged at VPN — day 1; not re-flagged here).

**Refs**: → `components.md`

### Monitoring (Data Removal) — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17676-9753&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Safety Monitoring"
2. Tabs (sticky)                                       ← VPN / Data Removal (selected) / Dark Web Monitoring
3. Hero / Feature  `active/data-removal`               ← H4 label "Total Removed" + Display-1 "276" + Status pill "Next scan Oct 12" + 5-row category bar list + stacked-area chart
4. ┌─ Group: Automation Packs ───────────────────────
   │  Section Header  `default`
   │  - Card / Feature  `automation` ×2                (Essential · Remove from major brokers — Lexisnexis.com + The Real Yellowpages — caption "3,232 users use this pack" below each card)
   │  └ footer CTA: Footer `card-section`, "See all"
5. ┌─ Group: Scan History ───────────────────────────
   │  Section Header  `default`
   │  Divider "In Progress" + List Item `progress` ×1  (HighSchool Alumni · 2 of 3 · brand-orange bar)
   │  Divider "Yesterday"   + List Item `progress` ×3  (HighSchool Alumni · Completed ×2 / HighSchool Alumni · No record · Completed)
   │  └ footer CTA: Footer `card-section`, "See all history"
6. Footer / `faq`  (feature-tinted)                    ← 4 cards; same monitoring tokens
```

**Tokens**
- Navigation, Tabs: same as Monitoring (VPN) — day 1.
- Hero `active/data-removal` (defers to Hero / Feature §13): container `--ct-bkgd-02`, padding-block `--ct-spacing-40`, gap `--ct-spacing-40`. Stats column 354px raw. Label `--ct-text-h4-*` capitalize. Number `--ct-text-display-1-*` (72px). Status pill defers to Label §3 `status/card`. Category bar list 5 rows: label `--ct-text-body-*`, bar 208×3px raw with raw category hexes (`#00c49a, #faa542, #719a03, #e1473f, #003ab8`) — no tokens (see Decisions / §13). Stacked-area chart h-233px raw, same 5 raw hexes.
- Automation Packs (Card / Feature §11 `automation`): card surface `--ct-monitoring-container-02` (#291132), radius `--ct-spacing-20`, width 314px raw, horizontal scroll with `--ct-spacing-8` gap. Header: pack name `--ct-text-body-*` `--ct-text-primary` (cream via local `data-theme="dark"`); right-aligned counter "3 automations" `--ct-text-body-small-*`. Title `--ct-text-h2-serif-*`?? — wait, §11 automation says title is body 16px capitalized 2-line — verify against §11. Two `contact` rows with 40×40 Brand Logo avatars. Footer `card-section` "See Details". Caption below each card: `--ct-text-body-small-*` `--ct-text-secondary`, "3,232 users use this pack".
- Scan History: Section Header `default`. Date Dividers (`In Progress`, `Yesterday`) defer to Divider §2 (`--ct-bkgd-01` band, body-small label). List Item `progress` rows defer to §6: surface `--ct-bkgd-02`, padding `--ct-spacing-20`, leading 40×40 brand-logo avatar (Hinge), title body + meta body-small `--ct-text-secondary`. Progress bar 8px raw, track `--ct-bkgd-01`, **fill `--ct-brand`** (#ff550c — the §6 spec; NOT `--ct-status-success-solid` like Activities).
- Footer `card-section`: top hairline `--ct-divider`, body-link "See all" / "See all history".
- Footer / `faq` (feature-tinted): same monitoring tokens as VPN — day 1.

**Decisions**
- **Hero matches Hero / Feature §13 `active/data-removal` exactly.** Display-1 "276" + Status pill ("Next scan Oct 12") + 5-row category bar list + stacked-area time chart. Don't reach for Simula on the 276 — even very large numbers stay sans (§13 Don't #1).
- **The 5 category hexes are illustration, not chrome.** `#00c49a` (Email) / `#faa542` (Family) / `#719a03` (Name) / `#e1473f` (Phone) / `#003ab8` (Address) — none of these resolve to existing `--ct-*` tokens. Per §13 / SKILL.md §2.1, don't approximate with the closest token; surface a request to add a category-color palette to Figma and re-export.
- **The 5-category breakdown lives INSIDE the hero, not as a separate group.** Day-1 ("what was found") rendered the same five categories as a standalone stat-row group with leading dots; on 1-year, those rows are compressed into the hero's category-bar visualization slot. The two patterns are NOT both shown on the same screen.
- **Automation Packs uses Card / Feature §11 `automation` ×2.** The category-tinted dark surface (`--ct-monitoring-container-02`) is the sanctioned use of monitoring tokens on a feature card per §11 — this is the one place Card / Feature is allowed to consume `--ct-monitoring-*`. The "3,232 users use this pack" caption sits below each card (not a §11 slot — verify if it should be promoted into the spec).
- **Scan History progress fill = `--ct-brand` (orange), NOT `--ct-status-success-solid`.** This screen tracks the List Item §6 default; the green-fill rule is Activities-only. Don't unify.
- **Closes with `Footer / faq` (feature-tinted), no `Footer / impact`.** Same closer choice as VPN — 1 year. Cross-cutting #3.

**Refs**: → `components.md`

---

### Guard — day 1

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17732-6162&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Spam Guard"
2. Tabs (sticky)                                       ← Call Guard (selected) / SMS Guard / Email Guard
3. Hero / Feature  `intro/call-guard`                  ← banner-tinted illustration band + kicker "Set up · 2 minutes" + H1 title "Block suspicious calls / in real time" + Primary CTA "Get up Call Guard"
4. Footer / `faq`  (feature-tinted)                    ← 4 cards; band `--ct-guard-container-02`, cards `--ct-guard-container-01`
```

**Tokens**
- Navigation `top_bar/page`: title "Spam Guard", `--ct-text-h2-serif-*` (Simula 24), `--ct-text-primary` on the page's banner-tinted outer surface (`--ct-banner-container` cream).
- Tabs: same chrome as Monitoring (VPN) — day 1 — backdrop-blur 16px raw, bottom border `--ct-divider`, padding-top `--ct-spacing-48` / padding-inline `--ct-spacing-16` / gap 10px raw. Tap_item: `--ct-text-body-*` `--ct-text-primary`, padding-block `--ct-spacing-20`. Selected: bottom-border `--ct-cta-primary-container`. Inactive: `--ct-opacity-disabled`.
- Hero `intro/call-guard` (defers to Hero / Feature §13): container + illustration band `--ct-banner-container` (#dcd8cf cream). Illustration height 333px raw, 225.5×220 raster (`asset/call guard`) per §13. Text block padding-block `--ct-spacing-24`, padding-inline `--ct-spacing-20`, gap `--ct-spacing-24`. Kicker row gap 10px raw, label `--ct-text-body-small-*` `--ct-text-primary`. Title `--ct-text-h1-*` capitalize `--ct-text-primary`. CTA: defers to Button `text/primary` — uses default `--ct-cta-primary-container` (dark), label `--ct-cta-primary-text`.
- Footer / `faq` (feature-tinted): container `--ct-guard-container-02` (#5b3b0d). FAQ cards: surface `--ct-guard-container-01` (#996820). Section title cream via local `data-theme="dark"`. FAQ card kicker `--ct-text-body-small-*` `--ct-text-ai-secondary` (#dcd8cf — NOT `--ct-brand`). FAQ card headline `--ct-text-h2-serif-*` `--ct-text-ai-primary`. Trailing `Button_Icon/Secondary` (48×48, `action/arrow_right`). Container padding-bottom `--ct-spacing-240`.

**Decisions**
- **Hero matches Hero / Feature §13 `intro/call-guard` exactly.** Banner-tinted illustration band on top, kicker row + 2-line H1 title + full-width Primary CTA below. Per §13, Guard's Primary CTA uses the default `--ct-cta-primary-container` (dark) — there is no `--ct-guard-container-*` CTA override (unlike `intro/vpn`, which uses `--ct-monitoring-container-02` for the CTA).
- **Page title is "Spam Guard", not "Guard".** Mirrors the Monitoring screen's "Safety Monitoring" pattern — internal feature name vs user-facing page title. The 3 tabs (Call Guard / SMS Guard / Email Guard) live below and switch sub-screens.
- **FAQ band feature-tinted with Guard tokens.** Container `--ct-guard-container-02`, cards `--ct-guard-container-01`, kickers `--ct-text-ai-secondary`. Same pattern as Monitoring's feature-tinted FAQ — already flagged at VPN — day 1 as conflicting with components.md §9 Don't #8.
- **No In Progress / list / history sections on Guard day 1.** Same minimalism as VPN day 1: Nav → Tabs → Hero → FAQ. The hero is the day-1 promise (cross-cutting #1).

**Refs**: → `components.md`

### Guard — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17732-6700&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Spam Guard"
2. Tabs (sticky)                                       ← Call Guard (selected) / SMS Guard / Email Guard
3. Hero / Feature  `active/call-guard`                 ← H4 label "Calls Blocked" + Display-1 "324" + 9-bar bar chart card + Segment control (Week / Month / Year — Week selected)
4. ┌─ Group: Recent History ─────────────────────────
   │  Section Header  `default`
   │  Divider "Today"        + List Item `event` ×1   (Cloaked Support · CS initial avatar · Label "Voicemail")
   │  Divider "Feb 14, 2026" + List Item `event` ×1   (341-152-3523 · Unknown call · U initial avatar · Label "Missed Call")
   │  Divider "Feb 14, 2026" + List Item `event` ×1   (341-152-3523 · Medical scam · M initial avatar · Label "Missed Call")
   │  Divider "Feb 14, 2026" + List Item `event` ×2   (341-152-3523 · Medical scam · Hinge brand-logo avatar · Label "Missed Call")
   │  └ footer CTA: Footer `card-section`, "See all"
5. Footer / `faq`  (feature-tinted)                    ← 4 cards; same Guard tokens as day 1
```

**Tokens**
- Navigation, Tabs: same as Guard — day 1 (page title "Spam Guard").
- Hero `active/call-guard` (defers to Hero / Feature §13): container `--ct-bkgd-02`, **width 394px raw — 1px wider than the rest, preserve per §13**. Label `--ct-text-h4-*` capitalize. Number `--ct-text-display-1-*` (72px sans). Chart card: padding `--ct-spacing-20`, gap `--ct-spacing-24`. Bar chart 354×238px raw, 9 bars at 16×{100..184}px raw (illustration), 8 hairlines `--ct-divider` 0.5px raw between bars. Day labels (M T W T F S S): `--ct-text-link-*` `--ct-text-primary` at raw `opacity: 0.6` (no `--ct-opacity-*` match). Segment control: gap `--ct-spacing-16`, three items at 107/108/107 px raw, padding 10px raw + `--ct-spacing-12` block/inline, radius `--ct-spacing-16`. Selected: `--ct-cta-primary-container` + `--ct-cta-primary-text`; unselected: `--ct-cta-secondary-container` border + `--ct-text-primary` label.
- Recent History: Section Header `default` (`--ct-bkgd-02`, H4 capitalize). Date Dividers defer to Divider §2 (`--ct-bkgd-01` 28px band, body-small label). List Item `event` rows defer to §6: surface `--ct-bkgd-02`, padding `--ct-spacing-20`, gap `--ct-spacing-8`, leading 40×40 avatar (`Avatar_default_caller initicial` for Cloaked Support / U / M, `Brand Logo_Hinge` for the Hinge rows). Title body + meta body-small `--ct-text-secondary`. Trailing: Label badge per §6 ("Voicemail" / "Missed Call") — cream pill `--ct-bkgd-01`, h-32, padding `--ct-spacing-12`/`--ct-spacing-4`, radius `--ct-spacing-4`, body 16 `--ct-text-primary`. Bottom hairline `--ct-divider` between rows.
- Footer `card-section` "See all": top hairline + body-link.
- Footer / `faq` (feature-tinted): same Guard tokens as day 1 (`--ct-guard-container-02` band, `--ct-guard-container-01` cards, `--ct-text-ai-secondary` kicker).

**Decisions**
- **Hero matches Hero / Feature §13 `active/call-guard` exactly.** Don't reach for Simula on the 324 — Display-1 sans (§13 Don't #1). The 394px width (1px wider than other heroes) is the Figma master spec — preserve, don't normalize to 393.
- **Day labels use raw `opacity: 0.6`** (per §13). Not a token — only `--ct-opacity-disabled` (0.3) exists; surface a request before tokenizing.
- **Recent History trailing slot uses Label badge per List Item §6** ("Voicemail" / "Missed Call") — cream pill, NOT a Status pill (Label §3 status variants), because the value is a call-disposition tag, not a state. Don't substitute.
- **Avatar mix in Recent History rows**: `Avatar_default_caller initicial` for unknown / one-off contacts (CS, U, M) and `Brand Logo_Hinge` for branded entries — same row component, different leading slot per §6's `image: boolean` rule. The CS/U/M initials are full opacity cream on a brand-color background (per §6 caller-initial avatar).
- **Closes with `Footer / faq` (feature-tinted Guard), no `Footer / impact`.** Same closer choice as day 1. Cross-cutting #3.

**Refs**: → `components.md`

---

### Identity — day 1

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17794-10011&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Hide My Identity"
2. Tabs (sticky, 6 items)                              ← All (selected) / Phone / Email / Card / Password / Account — see Decisions
3. Hero / Feature  `intro/identity`                    ← full-bleed dark gradient + photo overlay (mix-blend screen) + autoplay video (mix-blend lighten) + cream H1 title "Never give away your / real information again" + cream Primary CTA "Get Started"
4. Footer / `faq`  (feature-tinted)                    ← 4 cards; band `--ct-identity-container-02`, cards `--ct-identity-container-01`
```

**Tokens**
- Navigation `top_bar/page`: title "Hide My Identity", `--ct-text-h2-serif-*` (Simula 24), `--ct-text-primary` resolved cream (the page outer surface inherits the hero's dark theme — see Decisions).
- Tabs: same chrome as the other feature pages (backdrop-blur 16px raw, bottom border `--ct-divider`, padding-top `--ct-spacing-48`, padding-inline `--ct-spacing-16`, gap 10px raw). 6 Tap_items: `--ct-text-body-*` `--ct-text-primary` (cream over the dark hero). Selected: bottom-border `--ct-cta-primary-container` (resolves cream under `data-theme="dark"`). Inactive: `--ct-opacity-disabled`.
- Hero `intro/identity` (defers to Hero / Feature §13): container 393×756 raw, `position: relative`, `overflow: clip`. Background = raw dual gradient illustration (`linear-gradient(180deg, #0a0a0a 8.69%, #353d45 50.30%, #ccced1 137.05%)` over `linear-gradient(90deg, #194945, #194945)`) — do not tokenize per §13. Photo overlay raw raster, `mix-blend: screen`, `opacity: 0.9` raw. Autoplay video `mix-blend: lighten`. Title `--ct-text-h1-*` capitalize `--ct-text-primary` (cream under `data-theme="dark"`). CTA: container `--ct-cta-primary-container` and label `--ct-cta-primary-text` — both invert under `data-theme="dark"` (cream container + dark label).
- Footer / `faq` (feature-tinted): container `--ct-identity-container-02` (#0e1f31). FAQ cards: surface `--ct-identity-container-01` (#193047). Kickers `--ct-text-body-small-*` `--ct-text-ai-secondary` (#dcd8cf). Headlines `--ct-text-h2-serif-*` `--ct-text-ai-primary`. Trailing `Button_Icon/Secondary`. Container padding-bottom `--ct-spacing-240`.

**Decisions**
- **Hero matches Hero / Feature §13 `intro/identity` exactly** — including the requirement that the hero (and the Nav + Tabs that overlay it) sits in `data-theme="dark"`. Under light theme the inverted CTA values flip wrong; the cream background of the page outer surface (`bg-bkgd_02`) is hidden under the absolutely-positioned hero on day 1 anyway.
- **Page title is "Hide My Identity", not "Identity".** Mirrors the Monitoring → "Safety Monitoring" / Guard → "Spam Guard" pattern: internal feature name vs user-facing page title. Use the user-facing string.
- **The 6-item filter strip is rendered as Tabs in the Figma master, but cross-cutting #8 calls for Segmented Control here.** All / Phone / Email / Card / Password / Account is a list filter (one list shown, narrowed by category), not a navigation switch between sub-screens — so cross-cutting #8 says Segmented Control. The Figma master uses the same Tabs strip as Monitoring / Guard (selected = bottom border, inactive = opacity-disabled). _Question for the user: is the Figma intentional (Tabs supersede Segmented Control on Identity for visual continuity), or should this be migrated to a Segmented Control / Control §5 instance per cross-cutting #8?_
- **No In Progress / list / history sections on Identity day 1.** Same minimalist day-1 structure as VPN day 1 / Guard day 1: Nav → Tabs → Hero → FAQ. Identity's "first item" surfaces in the *activated* state below.
- **FAQ band feature-tinted with Identity tokens** (`--ct-identity-container-02` / `_01`). Already-flagged conflict with components.md §9 Don't #8 — not re-flagged here.

**Refs**: → `components.md`

### Identity — activated

> Bridge state. User has just created their first identity item.

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17794-9584&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Hide My Identity"
2. Tabs (sticky, 6 items)                              ← All (selected) / Phone / Email / Card / Password / Account
   ⚠  Hero is REMOVED on activated state — does NOT match cross-cutting #1 — see Decisions
3. ┌─ Group: phone numbers ──────────────────────────
   │  Section Header  `default`
   │  - List Item  `contact`                           (Doordash · Restaurant · Hinge brand-logo avatar · 342-231-1234 trailing)
   │  └ footer CTA: Button `text/secondary`, "+ Create new number"
4. ┌─ Group: Emails ─────────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new email"
5. ┌─ Group: Cards ──────────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new card"
6. ┌─ Group: Passwords ──────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new password"
7. ┌─ Group: Accounts ───────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new account"
8. Footer / `faq`  (feature-tinted)                    ← 4 cards (same as Identity — day 1)
```

**Tokens**
- Navigation, Tabs: same chrome as Identity — day 1, but Tabs now sit on the cream `--ct-bkgd-01` page surface (no dark hero behind them) — title and tab labels resolve `--ct-text-primary` dark in light theme.
- Outer page surface: `--ct-bkgd-01` (cream). Section groups separated by `--ct-spacing-12` cream gaps.
- Section Header `default` (×5): surface `--ct-bkgd-02`, title `--ct-text-h4-*` capitalize, padding-top `--ct-spacing-40`, padding-bottom `--ct-spacing-12`, padding-inline `--ct-spacing-16`.
- List Item `contact` (Phone Numbers row): surface `--ct-bkgd-02`, padding `--ct-spacing-20`, gap `--ct-spacing-12`, leading 40×40 `Brand Logo_Hinge` avatar, title body + meta body-small `--ct-text-secondary`, trailing plain-text 172px raw right-aligned ("342-231-1234"), bottom hairline `--ct-divider`.
- "+ Create new X" Button `text/secondary` (×5): width 353px raw, height 56px raw, padding 10px raw, radius `--ct-spacing-16`, border `--ct-cta-secondary-container`, label `--ct-cta-secondary-text` body sans. Container surface `--ct-bkgd-02`, padding-block `--ct-spacing-16`.
- Footer / `faq` (feature-tinted Identity): same tokens as Identity — day 1 — `--ct-identity-container-02` band, `--ct-identity-container-01` cards, `--ct-text-ai-secondary` kicker.

**Decisions**
- **Activated state DROPS the hero entirely** — contradicts cross-cutting #1 ("Activated: hero is unchanged from day 1; the change is below"). For Identity, the moment the user creates their first item, the hero disappears and the page becomes the category list directly. _Question for the user: add an Identity exception to cross-cutting #1, or should the Figma master add the hero back to match #1 across all features?_
- **All 5 categories appear in activated state, not just the activated one** — also contradicts the existing block placeholder ("only the activated category is shown"). Each category renders its own Section Header + (optional rows) + Secondary "+ Create new X" footer button. Empty categories show only the button — that button doubles as the per-category empty-state nudge.
- **The "+ Create new X" Secondary button is the per-group footer CTA** (cross-cutting #4). When the category has rows, it remains as the last item in the group (create-another). When empty, it IS the only thing in the group.
- **The single populated row uses List Item §6 `contact` variant** — Brand Logo avatar + title (entity name) + meta (category descriptor) + plain-text trailing (the actual phone number). Not `progress` (Activities / Monitoring) or `event` (Guard).
- **Identity — activated is structurally a sparse Identity — 1 year** — same 5-category spine, same per-group "+ Create" footer, no hero in either. The difference between activated and 1-year is row density, not structure.
- **Section title casing is inconsistent in the Figma master** ("phone numbers" lowercase vs "Emails" / "Cards" / "Passwords" / "Accounts" title case). Section Header §7 applies CSS `capitalize`, so all should be sourced lowercase per SKILL.md §6.5 — flag the Figma drift on the title-case entries.

**Refs**: → `components.md`

### Identity — 1 year

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=17794-8810&m=dev

**Composition (stack)**
```
1. Navigation  `top_bar/page`                          ← title "Hide My Identity"
2. Tabs (sticky, 6 items)                              ← All (selected) / Phone / Email / Card / Password / Account
   ⚠  No hero (same as activated state)
3. ┌─ Group: Inbox  (NEW vs activated) ───────────────
   │  Section Header  `default`
   │  - List Item  `inbox` ×3                          (Shopping · "Your Lululemon order is placed" · sms icon trailing / Dr.Kim's office · "confirming your appointment Weds.." · email icon / Redfin · "We helped a marketing firm…" · email icon)
   │  └ footer CTA: Footer `card-section`, "See all"
4. ┌─ Group: phone numbers ──────────────────────────
   │  Section Header  `default`
   │  - List Item  `contact` ×3                        (Hinge · Social · 425-352-6234 / Craigslist · Shopping · 521-352-6234 / Doordash · Restaurant · 342-231-1234) — Brand Logo avatars
   │  - Button  `text/secondary`  "+ Create new number"
   │  └ footer CTA: Footer `card-section`, "See all"
5. ┌─ Group: Emails ─────────────────────────────────
   │  Section Header  `default`
   │  - List Item  `contact` ×3                        (Newsletter · Subscription · night.trip@cloak.id / Free Wifi · Wifi Service · wish.fish.dish@cloak.id / DHL Delivery · Shopping · Juie@cloak.id) — `Default_Identity/Authenticator` icon avatar
   │  - Button  `text/secondary`  "+ Create new email"
   │  └ footer CTA: Footer `card-section`, "See all"
6. ┌─ Group: Cards ──────────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new card"     ← no "See all" footer (empty)
7. ┌─ Group: Passwords ──────────────────────────────
   │  Section Header  `default`
   │  (no rows)
   │  └ footer CTA: Button `text/secondary`, "+ Create new password" ← no "See all" footer (empty)
8. ┌─ Group: Accounts ───────────────────────────────
   │  Section Header  `default`
   │  - List Item  `contact` ×3                        (Target · Shopping / Twitch · Entertainment / Amazon · Shopping) — single-line entries (no meta), trailing category text
   │  - Button  `text/secondary`  "+ Create new account"
   │  └ footer CTA: Footer `card-section`, "See all"
9. Footer / `faq`  (feature-tinted)                    ← 4 cards (different copy from day 1)
```

**Tokens**
- Navigation, Tabs: same chrome as Identity — activated. Outer page surface `--ct-bkgd-01` (cream); section group surfaces `--ct-bkgd-02`.
- Section Header `default` ×6: surface `--ct-bkgd-02`, title `--ct-text-h4-*` capitalize.
- List Item `inbox` (Inbox group, ×3): surface `--ct-bkgd-02`, padding `--ct-spacing-20`. Leading 40×40 `Avatar_Category` SVG. Title body + meta body-small `--ct-text-secondary`. Trailing 24×24 type icon (`feature/identity/sms` or `feature/identity/email`) per List Item §6 trailing-icon slot.
- List Item `contact` (Phone Numbers / Emails / Accounts): surface `--ct-bkgd-02`, padding `--ct-spacing-20`. Leading 40×40 — Brand Logo avatar (Phone Numbers, Accounts) or `Default_Identity/Authenticator` icon avatar (Emails). Title body + meta body-small `--ct-text-secondary` (or single-line for Accounts). Trailing plain-text right-aligned per §6.
- Button `text/secondary` (×5 "+ Create new X"): width 353px raw, height 56px raw, padding 10px raw, radius `--ct-spacing-16`, border `--ct-cta-secondary-container`, label `--ct-cta-secondary-text` body sans. Wrapper padding-block `--ct-spacing-16`.
- Footer `card-section` "See all" (×4: Inbox / Phone Numbers / Emails / Accounts): top hairline `--ct-divider`, body-link 12px `--ct-text-primary`, height 50px raw.
- Footer / `faq` (feature-tinted): same Identity tokens as day 1 / activated (`--ct-identity-container-02` band, `--ct-identity-container-01` cards, `--ct-text-ai-secondary` kicker, `--ct-text-ai-primary` Simula H2 headline). Container padding-bottom `--ct-spacing-240`.

**Decisions**
- **No hero on Identity — 1 year, same as activated state.** Cross-cutting #1's hero-evolution rule (day 1 → activated → 1 year, slot preserved) does not apply to Identity — the hero is dropped at activation and never returns. Already flagged at activated; same exception applies here.
- **A 6th group — Inbox — appears at 1-year that didn't exist on activated.** It surfaces messages received against the user's created identities (Lululemon order to a fake email, Dr.Kim's appointment to a fake phone, etc.). Inbox is the only read-only category — no "+ Create new" button, just rows + `card-section` "See all" footer.
- **Per-group structure varies by row count.** Populated groups: rows → "+ Create new X" Secondary button → Footer `card-section` "See all". Empty groups (Cards, Passwords): just "+ Create new X" with no `card-section` footer (cross-cutting #4 — nothing to navigate to). The "+ Create new" button doubles as group footer when empty and as create-another row when populated.
- **The `contact` List Item variant adapts per category** — Brand Logo avatars for branded entities (Hinge, Doordash, Target, Twitch, Amazon, Craigslist), `Default_Identity/Authenticator` icon avatar for non-branded fake emails (Newsletter, Free Wifi, DHL Delivery). Same component, leading-slot type swap per §6's `image: boolean` toggle.
- **Accounts rows are single-line (no meta) with trailing category text** — different from Phone Numbers / Emails (which have a category meta line). The trailing slot here is content-driven plain text per §6, rendering "Shopping" / "Entertainment" / "Shopping" instead of the URL/handle.
- **Section title casing remains inconsistent in the Figma master** ("Inbox" / "phone numbers" / "Emails" / "Cards" / "Passwords" / "Accounts"). Section Header §7 applies CSS `capitalize` — source naturally lowercase per SKILL.md §6.5.
- **Closes with `Footer / faq` (feature-tinted Identity), no `Footer / impact`.** Same closer choice as day 1 / activated.

**Refs**: → `components.md`

### Guard — setup (call protection)

**Figma**: https://www.figma.com/design/k0n0CNGfk4ie9Vb74byl9v/Playlist-%E2%80%94-Toolkit?node-id=18556-7255&m=dev

**Composition (stack)**
```
1. ┌─ Progress row ───────────────────────────────────
   │  - Progress bar  (7-segment, seg 1 filled)        ← undocumented; see Decisions
   │  - Button  `icon-secondary/small`  `action/close` (48×48 trailing, right-aligned via space-between)
2. Title block                                         ← H1 "Choose your call protection" + body subtitle
3. ┌─ Group: Protection options ───────────────────────
   │  - Selection card  `selected`   (Full Protection · Forward all calls for maximum protection)
   │  - Selection card  `default`    (Smart Protection · Only forward when busy or unavailable)
4. Button  `text/primary`  "Continue"                  ← full-width, pinned near bottom (56px tall)
```

**Tokens**
- Outer surface: `--ct-bkgd-01` (resolves dark #141410 under `data-theme="dark"` — the whole screen is dark).
- Progress row: padding-top `--ct-spacing-48`, padding-bottom `--ct-spacing-8`, padding-inline `--ct-spacing-16`; row gap `--ct-spacing-4` between segments; segment height 4px raw (no `--ct-spacing-4` line-height token — 4px is the spacing value used as a height); each segment width `flex: 1` across a 305px raw track. Active segment fill `--ct-text-primary` (cream); inactive segments fill `--ct-graph-background` (white-05 in dark).
- Close button: defers to §1 `icon-secondary` 48×48 round, glyph `action/close`. The stroke is bundled in the SVG asset per §1's icon-stroke caveat.
- Title block: width 361px raw; internal gap `--ct-spacing-24`. Title (`H1`) `--ct-text-h1-*` capitalize, `--ct-text-primary`. Subtitle (`body`) `--ct-text-body-*` `--ct-text-secondary`, width 268px raw.
- Title-block-to-selection-card-group gap: 78px raw (computed from Figma's absolute layout — title block ends ~404, selection cards begin at 482; no matching `--ct-spacing-*` token, so raw).
- Selection card group: width 361px raw; gap `--ct-spacing-16`. Both cards defer to Selection card §16 — surface `--ct-bkgd-02` (resolves #1b1b18 in dark), padding-inline `--ct-spacing-16`, padding-block `--ct-spacing-32`, gap `--ct-spacing-16`, border-radius `--ct-spacing-20`. `selected` card adds `1px` solid `--ct-text-primary` border + checkbox tile `--ct-cta-primary-container` (cream in dark) with white 16×16 check glyph. `default` card has no border + checkbox tile `--ct-graph-background`, empty.
- Continue CTA: defers to §1 `text/primary`. Container `--ct-cta-primary-container` (cream in dark), label `--ct-cta-primary-text` (resolves near-black #141410 — paired-for-contrast under dark theme), padding `--ct-spacing-16`, border-radius `--ct-spacing-16`. Height 56px raw, width 361px raw.

**Decisions**
- **Progress bar is undocumented in components.md.** This is the first explicit sighting of the 7-segment onboarding progress bar (segments are `flex: 1` width × 4px height, gap `--ct-spacing-4`, active fill `--ct-text-primary` / inactive `--ct-graph-background`). The earlier attempt to spec it via Figma node `15996:3532` failed (`get_design_context` errored on that node). _Question for the user: promote the progress bar to a new component spec — likely under §10 Navigation alongside `top_bar/*` — or accept inline for now and revisit?_
- **No `top_bar` chrome.** Setup screens replace the page header with the progress row + close button. The close (×) is the only escape affordance — there is no Simula page title and no "Back" arrow. This is a deliberate onboarding-flow pattern (steps own the chrome, not navigation).
- **Pre-selection is intentional.** The first card (`Full Protection`) is `selected` on entry; the user dissents by tapping `Smart Protection` rather than affirming the default. Don't flip this to no-selection on render — the spec is opinionated.
- **Cards are mutually exclusive (radio behavior, checkbox UI).** Selection card §16 has no `radio` variant; it uses the checkbox tile as the affordance, and the surrounding flow enforces single-select. Don't substitute a radio component — the visual signature is the checkbox + border swap (per §16's selected-vs-default treatment).
- **No closer band (no `Footer / faq`, no `Footer / impact`).** Cross-cutting #3 ("every page ends with one closer — faq OR impact") is scoped to main-nav screens. Setup screens close with the primary CTA — the "Continue" button is the closer.
- **Outer surface is dark, not feature-tinted.** Even though this is Call Guard's onboarding, the surface is `--ct-bkgd-01` resolved dark, not `--ct-guard-container-*`. Feature identity appears later (day 1 hero / FAQ band); the setup flow is neutral chrome so steps from any feature can share the same shell.

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
