# Cloaked — LLM Instructions

## Philosophy

Cloaked is a calm, editorial, document-like product designed for users around 55 years old who are buying a service — not adopting a tool.

Core principles:

1. Plain language over technical terms. Say "Block scam calls," not "configure VPN tunnel." Pair technical names (VPN, eSIM) with plain-English descriptions on first use.
2. Calm layout, not a dashboard. Generous breathing room, hero numbers, serif headlines. The screen should feel like reading a Sunday paper, not operating a tool.
3. One unambiguous primary action per screen. Don't make users compare two same-weight buttons. The black primary button is what to tap next.
4. Layered surfaces, no borders. Cream (`--ct-bkgd-01`) is the page floor; white (`--ct-bkgd-02`) sheets sit on top. Sections separate with a 12pt cream gap — never with shadows, borders, or rounded outlines.
5. One visible accent at a time. Black is the default CTA. Brand orange (`--ct-color-brand`) is reserved for active states. Never both at once.
6. Serif for emotion, sans for facts. Simula is for page titles and FAQ headlines only. Everything else is SF Pro.
7. Numbers are heroes. Aggregate stats use Display 72px or H1 32px. The number is the page; the label is the footnote.
8. Trust the tokens. Never hand-pick hex values when a token exists. Source of truth: `tokens/*.css` files in this package.

## Naming Rules

All design tokens use the `--ct-` prefix (short for Cloaked Toolkit).

### Token categories

- `--ct-color-*` — Color primitives (16 tokens). Defined in `tokens/colors.css`. Never hand-pick hex; always reference these.
- `--ct-bkgd-*`, `--ct-text-*`, `--ct-cta-*`, `--ct-status-*`, etc. — Semantic theme tokens. Defined in `tokens/themes.css`. These flip between light and dark modes.
- `--ct-spacing-*` — Spacing tokens (4px–240px). Defined in `tokens/numbers.css`.
- `--ct-opacity-*` — Opacity tokens. Defined in `tokens/numbers.css`.
- `--ct-text-*-{family|weight|size|line-height|letter-spacing}` — Typography tokens. Defined in `tokens/typography.css`.
- `--ct-font-{sans|mono|serif}` — Font family fallback chains. Defined in `tokens/typography.css`.

### Theme selector

Themes are activated via the `data-theme` attribute on the root element:

```html
<html data-theme="light">
<html data-theme="dark">
```

There is no fallback. The `data-theme` attribute must be present.

### Special token groups

- `--ct-text-ai-*` — Reserved for fixed-dark surfaces (e.g., dark FAQ band, AI input field). These do not flip with the theme.
- `--ct-monitoring-*`, `--ct-guard-*`, `--ct-identity-*` — Category color tokens. Currently use raw hex values (not yet mapped to primitives). Treated as Cloaked product feature accents.

## When to use Kit voice

The "Kit voice" is the editorial, warm tone of the product — expressed visually through the Simula serif typeface. It's the one moment of emotional emphasis in an otherwise calm, sans-serif interface.

### Use Simula for

- Page titles (Serif H2, 24px) — every screen header.
- FAQ card titles in the dark FAQ band — actual questions ending in "?".

### Use SF Pro (sans) for everything else

- All body copy, labels, captions, sublabels.
- Section titles (H3, Title Case).
- Hero numbers (Display 1, Display 2, H1) — even very large numbers use SF Pro.
- Buttons, list rows, KPI strips, status pills.

### Tokens to use

- Simula: `--ct-text-h1-serif-*`, `--ct-text-h2-serif-*`
- SF Pro: `--ct-text-display-1-*`, `--ct-text-display-2-*`, `--ct-text-h1-*`, `--ct-text-h2-*`, `--ct-text-h3-*`, `--ct-text-body-*`, `--ct-text-body-small-*`
- SF Mono: `--ct-text-link-*`

### Rule of thumb

If you're unsure, default to SF Pro. Simula is the rare moment, not the default. A screen with Simula everywhere loses its editorial impact.

## When to ask the user

Default to acting on clear instructions. Ask only when continuing without input would lead to a wrong-by-design output.

### Ask when

- Theme is ambiguous. If the user requests a component but doesn't specify light or dark, ask which `data-theme` to assume.
- A token doesn't exist for the value. If the user asks for a color, size, or spacing that doesn't map to an existing token, ask whether to (a) use the closest existing token, (b) add a new token to the system, or (c) use a one-off value (discouraged).
- The component crosses unclear boundaries. If the request could reasonably mean two different components (e.g., "tab bar" — top TabStrip or bottom NavBottomBar?), ask which.
- Brand decisions are required. Microcopy ("what should this CTA say?"), iconography choice, or copy tone — defer to the user.

### Don't ask when

- The token system has a clear answer. Use the token. Don't ask "should I use `--ct-text-h1`?" if the spec says "page title."
- The user gave explicit values. Honor them. Don't second-guess.
- The choice is purely cosmetic with no design implication. Pick a sensible default and proceed.

### Format of the question

Be specific. Bad: "Which theme?" Good: "Should this card use `data-theme=\"light\"` (default app surface) or `data-theme=\"dark\"` (AI band / FAQ section)?"

## Forbidden patterns

These are non-negotiable. Violating them produces output that is wrong-by-design, regardless of how reasonable it might look.

### Tokens

- Don't hand-pick hex values when a token exists. Always reference `--ct-color-*` or `--ct-bkgd-*`, never `#FF550C` or `#0B0B0A` inline.
- Don't invent new tokens. If a value isn't in `tokens/*.css`, ask the user before adding it. New tokens require Figma source.
- Don't apply `--ct-text-ai-*` outside fixed-dark surfaces. These are for the dark FAQ band and AI input only — they don't flip with the theme.
- Don't omit `data-theme`. The attribute must be present on the root element. There is no fallback.

### Typography

- Don't use Simula for body copy, labels, or numbers. Simula is for page titles and FAQ headlines only.
- Don't bold text to create hierarchy. All weights are 400. Use size + family + color for hierarchy.
- Don't hand-type ALL CAPS labels. Section titles render in Title Case via CSS `text-transform: capitalize`. Source strings should be written naturally ("recent locations"), not "RECENT LOCATIONS".

### Layout & surfaces

- Don't add drop shadows to cards. Separation comes from layered surfaces (cream + white) and 12pt gaps, not shadows.
- Don't add borders or rounded outlines to separate sections. Use the 12pt cream gap.
- Don't put cream above the page header. The header sits on the same white surface as the first section beneath it.
- Don't add `chevron.right` to list rows. The list itself is the affordance. The right slot is for content (value, status, meaningful icon) or empty.

### Components

- Don't render simulated iOS status bars (fake "9:41", signal/wifi/battery icons). The system draws those at runtime.
- Don't replace feature signatures with generic icons. Each Cloaked feature has a specific visual signature (map, shield, etc.) that anchors recognition. (Detailed in `components.md` when complete.)

### Copy

- Don't write technical jargon. "Block scam calls," not "configure VPN tunnel." "Hide your real phone number," not "provision a phone alias."
- Don't use "Loading…" Use a status row with a progress bar + state label.
- Don't write apologetic empty states. No "Nothing here yet." Use a hero illustration + kicker + Simula sentence + one CTA.
