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
- **Home**: day 1, 1 year
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

3. **FAQ at the bottom, colored by feature**
   Every page ends with the FAQ section. **The FAQ card color matches its feature's identity color.** Never use a generic FAQ color.

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

### Home — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _What's in the hero (promise + single CTA)._
- _Why warm neutral, not a feature color (Home summarizes all features)._

**Refs**: → `components.md`

### Home — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _What replaced the day 1 hero (score, "Actions taken" big number, breakdown)._
- _Note: Home aggregates all features. It does not own a single feature color._

**Refs**: → `components.md`

---

### Activities — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero is orange gradient with hero number 245 + "Places data is exposed" label._
- _"Activity history will show here" placeholder. What's deferred until 1 year._

**Refs**: → `components.md`

### Activities — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero number jumps to 4,216. 3-tile breakdown appears below._
- _New stacks: Scan History group with "See more" footer, Social Proof block with "Explore tools" CTA._

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