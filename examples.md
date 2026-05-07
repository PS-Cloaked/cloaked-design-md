# Examples

# Examples

> Bridge between the design system and real screens.
> **What this file does**: shows how the main navigation tabs are assembled — how cards stack, how groups end, and how each feature's hero evolves from day 1 to 1 year.
> **What this file does NOT do**:
> - Define components → see `components.md`
> - List token values → see `tokens.css`
> - State design rules → see `CLAUDE.md`

If you're about to add a token or define a component here, stop. You're in the wrong file.

---

## How to use this file

When designing or coding a new screen for Cloaked:

1. **Identify the section** — Home / Activities / Monitoring / Guard / Identity, or new.
2. **Identify the state** — day 1 (sparse, no data yet) or 1 year (dense, accumulated data)?
3. **Find the closest example below.** Use its **Composition** as your starting skeleton — including the stack groupings and section footers.
4. **Open the Figma node via MCP** (URL is in each block). Verify component names, spacing, and token usage before writing code.
5. **Read the Decisions section.** Apply the bans ("do not...") strictly.
6. **Stop and ask** if you need a component or token that doesn't exist in `components.md` / `tokens.css`.

---

## Cloaked's main navigation tabs

These are the screens reached from the bottom navigation. They are the **spine** of the product.

| Tab | What it does |
|-----|--------------|
| **Home** | Dashboard. Surfaces score, summary of all features, recent activity. |
| **Activities** | Every security action Cloaked takes — removals, scans, blocks. |
| **Monitoring** | VPN + data removal status. Where my data is, where it's been scrubbed from. |
| **Guard** | Spam management. Blocks suspicious calls, SMS, email. |
| **Identity** | Fake identity layer. Phone numbers, emails, cards, passwords, accounts that hide my real info online. |

---

## Cross-cutting patterns

Rules that apply to **every** screen below. Do not restate these in individual examples.

1. **Hero evolution: day 1 → 1 year**
   Every feature has the same evolution arc. The hero module is the same slot, but its content transforms:
   - **Day 1**: hero shows a **promise** — placeholder visual + single CTA ("Get up Call Guard", "Secure my connection", "Get Started").
   - **1 year**: hero shows **data** — large number, chart, or map proving the promise was kept.
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
   If `ListItem` (or any component) can carry the data, use it. Do not build "activity row", "scan row", "session row".

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

Day 1 and 1 year of the same feature are placed **side by side** so the hero evolution is visible.

---

### Home — 1 year

> Home only exists in 1 year form. There is no day-1 Home — onboarding flows directly into the 1 year dashboard once data starts accumulating.

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. [ Header ]
2. ┌─ Group: ...
   │  ...
   │  └ footer CTA: ...
3. ...
```

**Tokens**
- _Surface, hero treatment, type scale. Not exhaustive._

**Decisions**
- _Why this composition. Bans go here. 3–6 bullets._
- _Note: Home aggregates all features. It does not own a single hero color._

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
- _What's in the hero slot now (placeholder/CTA)._
- _Why orange. What gets deferred until 1 year._

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
- _What replaced the day 1 hero (real number, breakdown)._
- _New stacks that appear (scan history group, social proof group)._

**Refs**: → `components.md`

---

### Monitoring — day 1

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Hero is the empty map + "Secure my connection" CTA._
- _Why purple._

**Refs**: → `components.md`

### Monitoring — 1 year

**Figma**: <!-- node-id -->

**Composition (stack)**
```
1. ...
```

**Tokens**
- _..._

**Decisions**
- _Map fills with location dots. Stat trio (Locations / Hours / Data used) appears below._
- _Tabs (VPN / Data Removal / Dark Web) are navigational, not filters — use Tab, not Segmented Control._

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
- _Hero shows a sculpted illustration + "Get up Call Guard" CTA._
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
- _Hero becomes "Calls Blocked" number + week heatmap._
- _Recent History group (calls/SMS/email) appears below, with "See all" footer._

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
- _Hero shows a silhouetted figure + "Get Started" CTA._
- _Why dark blue._

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
- _No hero number — Identity is list-dominant. Categories (Phone / Email / Card / Password / Account) repeat the same group structure: header → ListItems → "+ Create new" button → "See all" link footer._
- _Filter chips at top use Segmented Control (filtering), opposite of Monitoring's Tabs (navigation)._

**Refs**: → `components.md`

---

## Sub-screens

The 9 blocks above cover the main nav tabs. Sub-screens (drill-downs from these tabs) are not listed individually — they inherit their parent feature's identity and follow the same patterns.

If a sub-screen breaks a pattern from above, that's a signal to **discuss before designing**, not to extend this file.

---

## Decision tree — which example should I look at?

| If you're building... | Look at |
|-----------------------|---------|
| A dashboard summarizing multiple features | Home — 1 year |
| A new feature's empty/onboarding state | Any "— day 1" block, closest in data type |
| A feature's data-rich state with progress/scans | Activities — 1 year |
| A spatial / map-led feature | Monitoring — 1 year |
| A feature centered on a single metric + time chart | Guard — 1 year |
| A list-dominant feature with repeating categories | Identity — 1 year |
| Anything else | Find the closest above, then ask before deviating |

---

## Maintenance

- **Source of truth is Figma.** When the Figma file changes, update this file.
- **Component names must match Figma component names exactly** — this file is read by AI tools via Figma MCP.
- **The 9-block scope is intentional.** These are the main nav tabs. Adding sub-screens here will dilute the patterns.
- **If you'd add a new block, ask first** whether it's a new pattern or an instance of an existing one.
