---
name: cloaked-toolkit
description: Use when working in the cloaked-design-system repo, generating UI with --ct-* tokens, building Cloaked components, or making design decisions about the Cloaked visual system. Enforces token discipline (no invented tokens, no raw hex outside Category_TBD), Simula scope (page titles and FAQ headlines only), theme rules (data-theme required, AI tokens are fixed-dark), and forbidden patterns (no chevrons on list rows, no card shadows, no simulated iOS chrome).
---

# Cloaked Toolkit — AI Entry Point

## 1. Required Reading

Before producing output, the agent must have access to:

| File | Role | Authority |
| --- | --- | --- |
| `tokens/colors.css` | Color primitives (16 tokens) | **Source of truth** for hex values |
| `tokens/numbers.css` | Spacing + opacity | **Source of truth** for numeric tokens |
| `tokens/themes.css` | Light + dark semantic tokens | **Source of truth** for theme mapping |
| `tokens/typography.css` | Text styles + `@font-face` | **Source of truth** for type tokens |
| `components.md` | Component specs | Components rulebook (16 components, all TBD) |
| `examples.md` | BAD / GOOD usage examples | Currently empty |

**Conflict resolution.** If two sources disagree:

1. Figma (when accessible via MCP) wins on visual specs.
2. `tokens/*.css` wins on token names and values.
3. This document wins on behavior rules.

If the conflict can't be resolved, **stop and ask the user**. Do not silently pick one.

---

## 2. Absolute Rules

These rules are non-negotiable. Violating any of them produces wrong-by-design output regardless of how reasonable it looks. Each rule has the same shape: **Rule → Why → Alternative**.

### 2.1 Don't invent new tokens

- **Rule.** Every `--ct-*` you write must already exist in `tokens/*.css`. Grep before writing.
- **Why.** Tokens are exported from Figma. A token you invent has no Figma source, will not survive the next export, and breaks theme flipping.
- **Alternative.** If a needed value is missing, stop. Tell the user the value is missing and ask whether to (a) use the closest existing token, or (b) add the token to Figma first and re-export.

### 2.2 Don't write raw hex (or px for spacing) when a token exists

- **Rule.** No `#FF550C`, `#0B0B0A`, `padding: 16px` inline. Use `var(--ct-color-brand)`, `var(--ct-bkgd-02)`, `var(--ct-spacing-16)`.
- **Why.** Raw values bypass the theme system. A hex pinned to "the dark cream color" silently turns wrong when the theme flips or the palette is retuned.
- **Alternative.** If you genuinely need a value not in the system, see §2.1. The only sanctioned raw hex is the **Category_TBD** group — see §9.1.

### 2.3 Don't modify component specs on your own

- **Rule.** When `components.md` (or any component spec) defines slots, sizes, layout, or anatomy, treat it as read-only. Don't "improve" it by adding a chevron, swapping a token, or renaming a slot.
- **Why.** Specs mirror Figma. Drifting from spec drifts from Figma, then production drifts from both.
- **Alternative.** Surface the proposed change to the user. If they agree, the change goes into Figma first, then back into `components.md`.

### 2.4 Don't use Simula for body, numbers, or labels

- **Rule.** Simula (serif) is only for page titles (`--ct-text-h2-serif-*`) and FAQ card titles (`--ct-text-h1-serif-*`). Everything else uses SF Pro (sans), even very large hero numbers.
- **Why.** Simula is the one moment of editorial emphasis in a calm, sans-serif product. Spreading it everywhere kills the contrast it exists to create.
- **Alternative.** Default to `--ct-font-sans` (or any non-`*-serif-*` text token). When unsure, sans is the safe choice.

### 2.5 Don't use bold to create hierarchy

- **Rule.** All weights in this system are **400**. Use size, family, and color to create hierarchy — never `font-weight: 700`.
- **Why.** Hierarchy is encoded in the text token (Display 1 vs Body, etc.). Bold short-circuits the system and produces visual noise that doesn't match Figma.
- **Alternative.** Pick a larger token, switch to Simula for the title slot, or change color to `--ct-text-primary` vs `--ct-text-secondary`.

### 2.6 Don't guess — ask

- **Rule.** When intent is ambiguous (which theme, which variant, which token, what should the copy say), stop and ask one specific question. See §8 for what counts as "ambiguous."
- **Why.** A wrong guess looks plausible and gets propagated. A clarifying question costs one message.
- **Alternative.** Frame the question concretely: not "which theme?" but "should this card use `data-theme=\"light\"` (default app surface) or `data-theme=\"dark\"` (AI band / FAQ)?".

### 2.7 Don't fabricate component variants

- **Rule.** When a component is spec'd in `components.md`, the only valid choices are the variants declared in its **Variants** table. Pick from the list. Don't compose a "muted icon button," "ghost CTA," or "filled gray pill" out of bare CSS tokens. This is the in-spec counterpart to §7.2 (which forbids inventing whole components when none is spec'd).
- **Why.** The variant list mirrors Figma. A CSS-only variant has no Figma source, will not survive the next export, and creates a quiet drift between code and design. Worse, the next agent looking at production sees a pattern they can't find in `components.md` and either copies the drift or guesses a third version.
- **Alternative.** If none of the declared variants fit, surface the case to the user with the gap named ("the help affordance reads as a double ring because the icon draws its own circle and `icon-secondary/large` adds another"). The fix is to add the variant to Figma → `components.md` → then use it. Not to invent it locally.

### 2.8 Don't compress the top header safe area

- **Rule.** The first interactive row of any screen header (back button, page title, trailing action) sits at minimum `--ct-spacing-40` from the top edge of the screen surface. Buttons live in the row beneath that 40px clear band, not inside it.
- **Why.** iOS notches, Dynamic Islands, and Android cutouts intrude on the top ~40px. Pushing the leading icon into that band hides it under system chrome at runtime — the screen looks fine in mockups and broken on device. On chromeless surfaces (e.g. modal sheets) the band still reads as breathing room before the title slot.
- **Alternative.** If you genuinely need the band reclaimed (immersive media, in-call surfaces), surface that specific case rather than tightening the default.

---

## 3. Namespace — what `--ct-*` means

All Cloaked tokens use the `--ct-` prefix (Cloaked Toolkit). The next segment encodes the role.

| Prefix | Role | Defined in |
| --- | --- | --- |
| `--ct-color-*` | Color **primitive** (raw hex). Don't use directly in components — go through a semantic token. | `tokens/colors.css` |
| `--ct-bkgd-*` | Background surfaces | `tokens/themes.css` |
| `--ct-text-primary` / `--ct-text-secondary` | Body / label text color | `tokens/themes.css` |
| `--ct-text-ai-*` | Text on **fixed-dark** surfaces (AI input, FAQ band) — does **not** flip with theme | `tokens/themes.css` |
| `--ct-text-<style>-{family\|weight\|size\|line-height\|letter-spacing}` | Typography. `<style>` ∈ `display-1`, `display-2`, `h1`, `h2`, `h3`, `h1-serif`, `h2-serif`, `body`, `body-small`, `link` | `tokens/typography.css` |
| `--ct-font-{sans\|mono\|serif}` | Font-family fallback chains | `tokens/typography.css` |
| `--ct-cta-{primary\|secondary}-{text\|container}` | CTA button color slots | `tokens/themes.css` |
| `--ct-status-{success\|fail}-{solid\|subtle}` | Status colors (semantic) | `tokens/themes.css` |
| `--ct-banner-*` | Banner colors | `tokens/themes.css` |
| `--ct-graph-background` | Graph fill background | `tokens/themes.css` |
| `--ct-divider` | Hairline divider color | `tokens/themes.css` |
| `--ct-brand` | Active-state accent (orange) | `tokens/themes.css` |
| `--ct-spacing-{4..240}` | Spacing scale (px) | `tokens/numbers.css` |
| `--ct-opacity-disabled` | Disabled opacity | `tokens/numbers.css` |
| `--ct-{monitoring\|guard\|identity}*` | Category accents — **raw hex, not yet on primitives**. See §9.1 | `tokens/themes.css` |

**Rule of thumb.** Components consume **semantic** tokens (`--ct-bkgd-*`, `--ct-text-primary`, `--ct-cta-*`). Primitives (`--ct-color-*`) are a backstage layer — only theme tokens reference them.

---

## 4. Token Reference (summary)

This section is **not** a catalog. The catalogs are `tokens/*.css`. Read those for the full list. This section flags the values you'll reach for most often and the rules that govern them.

### 4.1 Spacing — most-used values

The scale is `4, 8, 12, 16, 20, 24, 32, 40, 48, 56, 64, 72, 80, 96, 120, 240`. The five marked ★ cover ~80% of layout work; reach for these first.

| Token | Use |
| --- | --- |
| `--ct-spacing-8` ★ | Tight inner padding, icon-to-label gap |
| `--ct-spacing-12` ★ | **Section gap** (cream gap between sheets) — see §9.2 |
| `--ct-spacing-16` ★ | Standard inner padding (cards, list rows) |
| `--ct-spacing-20` ★ | Vertical row padding |
| `--ct-spacing-24` ★ | Section padding, large gaps |
| `--ct-spacing-{40..240}` | Hero spacing, large vertical rhythm |

**Rule.** No `margin`/`padding`/`gap` value goes inline as `px`. Always a token.

### 4.2 Typography — apply all five sub-tokens together

Each text style is a **set of five tokens**, not just a size. When you apply a style, apply all five — never cherry-pick `font-size` while leaving the other four to the browser default.

```css
/* GOOD */
.page-title {
  font-family: var(--ct-text-h2-serif-family);
  font-weight: var(--ct-text-h2-serif-weight);
  font-size: var(--ct-text-h2-serif-size);
  line-height: var(--ct-text-h2-serif-line-height);
  letter-spacing: var(--ct-text-h2-serif-letter-spacing);
}

/* BAD — partial application breaks the spec */
.page-title { font-size: var(--ct-text-h2-serif-size); }
```

The available styles are listed in `tokens/typography.css`. The role of each:

| Style | Role |
| --- | --- |
| `display-1` (72px) / `display-2` (48px) | Hero numbers — SF Pro |
| `h1` (32px) / `h2` (24px) / `h3` (20px) | Section / sub-section titles — SF Pro |
| `h1-serif` (32px) / `h2-serif` (24px) | **Simula only.** Page titles, FAQ headlines. See §2.4 |
| `body` (16px) / `body-small` (14px) | Body copy, labels |
| `link` (10px) | SF Mono — small monospace meta text |

### 4.3 Opacity

Only one opacity token exists: `--ct-opacity-disabled` (= `0.3`). Use it on disabled buttons, controls, and rows. Don't write `opacity: 0.5` or any other arbitrary value — disabled is the only state that has a token because it's the only state that needs one.

### 4.4 Color

Don't restate the catalog here. Read `tokens/colors.css` for primitives and `tokens/themes.css` for the semantic mapping. Two facts about the primitives that matter when reading them:

- `White-05`, `White-15`, `Black-05`, `Black-15` — the suffix is **alpha %**, not a hex variant. Same base hex with reduced opacity.
- `Green-02` and `Red-02` — same hex as `-01` at 10% alpha, intended for **subtle** status backgrounds paired with the solid `-01` foreground.

In components, **never reference `--ct-color-*` directly**. Use the semantic theme token (`--ct-bkgd-02`, `--ct-status-success-solid`, etc.). Primitives are backstage.

---

## 5. Theme

### 5.1 The `data-theme` attribute

Themes activate via a `data-theme` attribute on the root element:

```html
<html data-theme="light">
<html data-theme="dark">
```

**There is no fallback.** If `data-theme` is missing, no semantic token resolves and the page renders broken. Every example you generate must include the attribute.

### 5.2 Which tokens flip, which stay fixed

Most semantic tokens flip between light and dark. Two groups **do not flip** — they are pinned to a dark palette regardless of theme:

| Group | Tokens | Why |
| --- | --- | --- |
| AI surface text | `--ct-text-ai-primary`, `--ct-text-ai-secondary` | Always sits on a dark surface (AI input field, FAQ band) |
| AI input background | `--ct-bkgd-ai-input` | The AI input is **always** dark, even in light theme |

**Rule.** Don't apply `--ct-text-ai-*` or `--ct-bkgd-ai-input` to a surface that is not the AI input or the dark FAQ band. They will look correct in dark theme and broken in light theme — the tokens are doing their job; you put them in the wrong place.

### 5.3 Light vs dark — surface mapping

| Token | Light (`grey-01` / `white`) | Dark (`grey-05` / `grey-04`) |
| --- | --- | --- |
| `--ct-bkgd-01` | Page floor (cream) | Page floor (near-black) |
| `--ct-bkgd-02` | Sheet / card on top | Sheet / card on top |
| `--ct-text-primary` | Near-black on cream | Cream on near-black |
| `--ct-text-secondary` | Mid-grey | Mid-grey |
| `--ct-divider` | `black @ 15%` | `white @ 15%` |

For the full mapping, read `tokens/themes.css`. Don't memorize hex — reference tokens.

### 5.4 When the theme is ambiguous

If the user requests a component without specifying theme, **ask** (see §2.6, §8). Don't default to light silently. The wrong theme produces output that compiles fine but reads wrong on every screen it lands on.

---

## 6. AI Voice (Kit Voice = Simula)

The "Kit voice" is the editorial moment of the product. It exists in exactly two places. Use it there. Don't use it anywhere else.

### 6.1 Use Simula for

| Slot | Token | Size |
| --- | --- | --- |
| Page title (every screen header) | `--ct-text-h2-serif-*` | 24px |
| FAQ card title (the question itself, ending in `?`) | `--ct-text-h1-serif-*` | 32px |

That's the whole list. No other slot uses Simula.

### 6.2 Use SF Pro for everything else

- All body copy, labels, captions, sublabels.
- Section titles (`--ct-text-h3-*`, Title Case).
- Hero numbers — `--ct-text-display-1-*` (72px), `--ct-text-display-2-*` (48px), `--ct-text-h1-*` (32px). **Even very large numbers stay sans.**
- Buttons, list rows, KPI strips, status pills.

### 6.3 Use SF Mono for

- `--ct-text-link-*` only. Small (10px) meta text — link previews, monospace tags. Not for code blocks in product UI.

### 6.4 Rule of thumb

If unsure, sans. Simula is the rare moment, not the default. A screen with Simula in three places has lost its editorial impact — fix it by demoting two of them to SF Pro.

### 6.5 Section title casing

Section titles render in Title Case via CSS `text-transform: capitalize`. **Source strings must be written naturally** — `"recent locations"`, not `"RECENT LOCATIONS"` or `"Recent Locations"`. Don't hand-type the case; let CSS do it.

---

## 7. Working with Components

### 7.1 Current state

`components.md` is a **rulebook with 16 component slots — all bodies TBD**. The structure is fixed: 16 component names + a `Default visual properties` baseline + a per-component schema (Use / Anatomy / Variants / Sizing / Tokens / Don't / Figma).

What this means:

- The **list of valid Cloaked components is closed** at those 16. Don't invent a 17th — if a request doesn't fit one of the 16, surface it to the user.
- Each component's **body is still empty**. There is no written spec to copy from yet.
- Default visual properties live in `components.md` and apply unless a component explicitly overrides them.

When asked to build one of the 16, you have:

- Tokens (`tokens/*.css`) — definitive.
- This document (rules, namespace, theme).
- The schema in `components.md` (slot names, expected sections).
- Whatever the user tells you in chat.
- Figma (only if the user provides a link and Figma MCP is connected).

### 7.2 Behavior when no component spec exists

- **Don't fabricate a "Cloaked Button" / "Cloaked Card" from imagination.** No spec means no spec.
- **Ask the user for**: the variant they want, the slots/anatomy, the Figma link if one exists.
- **If they provide a Figma link and MCP is connected**: use `get_variable_defs` and `get_design_context` (forceCode) on the linked node. Skip `get_screenshot` — pixels don't carry token names.
- **If neither chat description nor Figma is available**: stop. Don't guess.

### 7.3 When component specs eventually land

When `components.md` (or per-component files) are written, the Absolute Rules (§2) still apply — especially §2.3 (don't modify specs). Treat any spec file as Figma's local mirror, not a draft.

### 7.4 Authoring component specs (rare)

If the user asks you to **write** a component spec into `components.md`, three rules govern the content:

1. **Reference a token** when the value lives in `tokens/*.css`. Write `var(--ct-spacing-16)`, not `16px`.
2. **Inline-explain** small atoms used in one place (e.g. a hairline divider, a one-off icon size). Don't link to a file that doesn't exist.
3. **Link to another component file** only when that file actually exists. Use a relative path.

Quality bar before saying done: every `--ct-*` token referenced must exist in `tokens/*.css` (grep to confirm). No raw hex outside `.css` blocks demonstrating a primitive's value.

---

## 8. Strict Behavior Rules — when to ask vs. proceed

### 8.1 Ask when

- **Theme is ambiguous.** User requested a component without saying light or dark.
- **No token matches the value.** Asked for a color, size, or spacing that doesn't map to any `--ct-*`.
- **Component boundaries unclear.** "Tab bar" could mean top TabStrip or bottom NavBottomBar — pick the wrong one and the layout breaks.
- **Brand decisions required.** Microcopy ("what should this CTA say?"), iconography choice, copy tone.

### 8.2 Don't ask when

- **A token clearly answers it.** Spec says "page title" → use `--ct-text-h2-serif-*`. Don't ask permission.
- **User gave explicit values.** Honor them. Don't second-guess `padding: var(--ct-spacing-20)` because you'd have picked 24.
- **Pure cosmetic with no design implication.** Pick a sensible default and proceed.

### 8.3 Question shape

Ask **one** specific question with concrete options. Not abstract.

```
BAD:  "Which theme do you want?"
GOOD: "Should this card use data-theme=\"light\" (default app surface)
       or data-theme=\"dark\" (AI band / FAQ section)?"
```

```
BAD:  "What about the spacing?"
GOOD: "Inner padding — --ct-spacing-16 (standard) or --ct-spacing-20
       (used on full-width list rows)?"
```

If three or more decisions are open, list them with concrete options each. Don't bundle into one vague question.

---

## 9. Forbidden Zones

These produce wrong-by-design output. They mirror parts of §2 but are concrete enough that a quick scan catches them.

### 9.1 Category_TBD — the only sanctioned raw hex

These nine tokens are currently raw hex in `tokens/themes.css` because they are not yet mapped to primitives:

```
--ct-monitoring, --ct-monitoring-container-01, --ct-monitoring-container-02
--ct-guard,      --ct-guard-container-01,      --ct-guard-container-02
--ct-identity,   --ct-identity-container-01,   --ct-identity-container-02
```

**Rule.** Reference these by token name, not by hex. They are a known TBD — eventually they'll be wired to primitives. **Do not** invent new category tokens, do not extend the pattern (`--ct-newcategory-*`), do not write the raw hex. If a fourth category is needed, stop and ask.

### 9.2 Layout — separation comes from the cream gap, not lines

- ❌ No drop shadows on cards.
- ❌ No borders or rounded outlines to separate sections.
- ❌ No cream above the page header — the header sits on the same white surface as the first section beneath it.
- ✅ Sections separate with `--ct-spacing-12` gap of `--ct-bkgd-01` (cream) between them.

### 9.3 List rows

- ❌ No `chevron.right` on list rows. The list is the affordance.
- The right slot of a row is for content (value, status, meaningful icon) or empty.

### 9.4 iOS chrome

- ❌ No simulated iOS status bar (`9:41`, signal/wifi/battery icons). The system draws those at runtime. Adding them is a tell that the screen is fake.

### 9.5 Feature signatures

- ❌ Don't replace a feature's visual signature with a generic icon. Each Cloaked feature has a specific signature (map, shield, etc.) — that's how recognition is anchored. (Specifics will land in `components.md`.)

### 9.6 Copy

- ❌ No technical jargon. "Block scam calls," not "configure VPN tunnel." "Hide your real phone number," not "provision a phone alias."
- ❌ No `"Loading…"`. Use a status row with a progress bar + state label.
- ❌ No apologetic empty states. No `"Nothing here yet."` Empty states are a hero illustration + kicker + Simula sentence + one CTA.

### 9.7 Typography (cross-reference)

See §2.4, §2.5, §6 — Simula scope, weight = 400, casing handled by CSS. These are the most-violated rules; double-check before handing back.

