---
name: cloaked-motion-system
description: Apply the Cloaked motion system to product UI, commercial, or brand identity animation work. Use when designing or specifying motion for buttons, modals, page transitions, lists, hovers, loaders, product films, logo lockups, type animation, or icons. Triggers on "what easing should I use", "how long should this animation be", "what's the right transition for", "design the motion for", "spec the animation for", "motion brief", "motion handoff", "tempo for this", "easing for this", or any motion design decision.
---

# Cloaked Motion System

A flexible motion design system for product UI, commercial work, and brand identity animation. Use it as the source of truth when designing or specifying any motion at Cloaked — interaction microcopy through full product films.

## Usage

```
/cloaked-motion-system component <name>     # Recipe lookup for a UI component
/cloaked-motion-system transition <type>    # Pick the right transition
/cloaked-motion-system sequence <scene>     # Plan staggering and hierarchy
/cloaked-motion-system spec <description>   # Generate a full motion spec sheet
```

When invoked, gather: what's changing, the size of the change, the priority/role, the personality, and whether it's part of a sequence. Then output durations in ms + frames at 30fps, bezier values for easing curves, transition type, and any expressions needed.

## Core principles

1. **Purposeful motion** — Every animation serves a function: directing attention, communicating relationships, signaling change, or expressing brand. No motion for motion's sake.
2. **Physical credibility** — Movement obeys mass, friction, and momentum. Even stylized motion borrows from physics.
3. **Hierarchy through tempo** — Faster motion is supporting. Slower motion is focal. Use this to direct the eye.
4. **Personality lives in the curve** — Easing carries more brand voice than any other parameter. Be intentional.
5. **Motion is editable** — Build animations so durations, easings, and offsets can be tweaked without rebuilding.

## What motion achieves

- **Hierarchy** — show what matters first
- **Continuity** — connect a "before" state to an "after" state so the user keeps context
- **Perceived performance** — fill wait times, soften loads
- **Brand expression** — easing + timing + character = brand
- **Storytelling** — in commercial work, motion is the narrative tool

## The 5 essential easings

Bezier values are CSS-style `[x1, y1, x2, y2]` — drop them straight into `cubic-bezier()`, Framer Motion `transition.ease`, SwiftUI `timingCurve`, or After Effects via the Flow plugin.

| Easing | Bezier | Use for | Personality |
|---|---|---|---|
| **Easy ease** | `0.42, 0, 0.58, 1` | Default for most UI motion | Balanced, neutral |
| **Expressive ease** | `0.65, 0, 0.35, 1` | Hero moments, brand-forward beats | Energetic, contrasted |
| **Enter ease** (out) | `0, 0, 0.35, 1` | Elements arriving on screen | Soft landing |
| **Exit ease** (in) | `0.65, 0, 1, 1` | Elements leaving screen | Decisive exit |
| **Linear** | `0, 0, 1, 1` | Loops, mechanical motion, sheens | Constant, neutral |

**After Effects Speed Graph translation:**

- Easy ease → Default `Easy Ease` (F9), 33% influence both sides
- Expressive ease → 50% influence both sides + boost outgoing/incoming velocity
- Enter ease → 75% incoming, 0% outgoing (slow arrival)
- Exit ease → 0% incoming, 75% outgoing (slow departure)
- Linear → toggle keyframe interpolation to Linear

Plugin shortcut: install **Flow** to paste bezier values directly. Use **EaseCopy** to clone curves between properties.

## 3 durations (at 30fps)

| Movement size | Quick | Standard | Slow |
|---|---|---|---|
| Small (UI feedback, hover, press, micro) | 100ms / 3f | 200ms / 6f | 300ms / 9f |
| Medium (component, modal, card) | 200ms / 6f | 400ms / 12f | 600ms / 18f |
| Large (page, full-screen, hero reveal) | 400ms / 12f | 600ms / 18f | 1000ms / 30f |

For commercial / film work, scale durations up: small beats 8-12f, medium 18-30f, large 30-90f. Anticipation beats 6-12f. Holds 12-24f.

For 24fps (film output), divide frame counts by 1.25. For 60fps (high-refresh UI), multiply by 2.

## Transitions (when to use which)

| Transition | When | Easing | Duration |
|---|---|---|---|
| **Still fade** | Same element, internal state change (data load, image swap) | Easy | Standard |
| **Sliding fade** | Element arriving from below or side; lists | Easy | Quick-Standard |
| **Window zoom** | Element expands into a new view (card → detail) | Expressive | Slow |
| **Window wipe** | Edge-anchored container reveals more content (drawer, panel) | Easy | Standard |
| **Scale** | Press feedback, attention micro-animation | Exit | Quick |
| **Human motion path** | Long traversals — curve, not straight line | Expressive | Slow |

**Window zoom rule:** Always zoom from the user's anchor point (where they tapped). Never zoom into the center of the screen — preserves spatial continuity.

**Human motion paths:** For traversals over long distances, use a slight Bezier curve rather than a straight line. People move in arcs.

## Sequence

### Delays between elements

| Type | Delay | Frames @30fps | Use for |
|---|---|---|---|
| Tight | 33ms | 1f | Groups treated as one unit (equal-priority grid items, a tight motif) |
| Standard | 100ms | 3f | Sequential reveals (list items, body sections, content blocks) |
| Emphasized | 150ms | 5f | Hero/title beats, the start and end of a sequence |

### Hierarchy in 3 steps

1. **Load the base UI first** — Header, nav, structural elements appear with little to no motion (or a quick fade). The shell is there before content arrives.
2. **Stagger meaningfully** — Content moves in the direction of intended scroll/read (top-to-bottom, left-to-right). Don't stagger against reading flow.
3. **Finish with a focal point** — The primary CTA or hero element gets the longest, most expressive entrance. The eye should land here last.

### Hinting direction

- **Scrolling hints**: Tight delays + slight movement in scroll direction (e.g., 4-6px pre-shift)
- **Diagonal grid stagger**: Top-left → bottom-right matches reading flow; bottom-right → top-left feels wrong unless you have a narrative reason
- **Don't stagger** left/right when content is flush full-width — looks like a timing bug

## Component recipes (UI cookbook)

| Component | Easing | Duration | Transition | Notes |
|---|---|---|---|---|
| Button (tap response) | Exit | Quick (small) | Scale 100→97→100 | 0-frame hold at peak |
| Floating container open | Exit | Standard (medium) | Window zoom from anchor | Anchor at parent |
| Edge container (drawer) | Easy | Standard (medium) | Window wipe | Mask wipe from edge |
| In-line card expand | Easy | Standard (medium) | Window wipe | Sibling auto-push |
| Hover (small element) | Easy | Quick (small) | Scale 100→110% | — |
| Hover (medium image) | Easy | Quick-Standard | Scale 100→103% | Container clips overflow |
| Hover (hero image) | Easy | Quick-Standard | Scale 100→101% | — |
| List/grid reveal | Easy | Quick (small) | Slide fade up + 100ms stagger | Direction = scroll direction |
| Full-screen expansion | Expressive | Slow (large) | Window zoom + curved path | 600-1000ms |
| Partial-screen expansion | Easy | Slow (medium) | Window zoom | 600ms |
| Page push | Expressive | Slow (large) | Slide horizontal + slight scale | 600-800ms |
| Modal sheet (bottom-up) | Enter | Standard (medium) | Slide from bottom | 300-400ms |
| Modal prompt (centered) | Exit | Standard (medium) | Scale 90→100 + fade | 200-300ms |
| Auto scroll (long) | Expressive | Slow | — | Custom bezier per scroll length |
| Auto scroll (short) | Expressive | Standard | — | 400ms |
| Horizontal gallery | Expressive | Standard-Slow | Slide horizontal | Add inertia tail |
| Toggle / micro-interaction | Easy | Quick (small) | Position + scale | 100-200ms |

Press scale percentages: small button 90%, standard button 97%, image 97-99%. Use Easy ease, Quick duration.

## Performance & feedback

### Loaders (in order of severity)

- **Bouncy ball** — Short waits where the next screen is preparing
- **Inline bouncy ball** — Buttons mid-action (e.g., submitting)
- **Pull ring** — Pull-to-refresh
- **Strip loader** — Background activity, doesn't block UI
- **UI skeleton** — Page shell appears instantly while content loads (grey blocks; replace via fade)
- **Media skeleton** — Stagger media tiles to imply hierarchy when content arrives

## Commercial / storytelling motion

For product films, social cuts, brand pieces, sizzle reels, and any motion work where there's a narrative arc, not just a UI state change.

### The 6 classic principles (applied)

1. **Anticipation** — Tiny prep movement before the main action (a 6-frame backwards push before a forward leap). Sells the energy.
2. **Follow-through & overshoot** — Things don't stop on target; they overshoot 5-15% then settle. Use a wobble curve or inertial bounce.
3. **Squash & stretch** — Volume-preserving deformation under acceleration. Subtle for product (1-3%), generous for character (10-30%).
4. **Slow in / slow out** — The Expressive ease in your kit.
5. **Arcs** — Real movement curves. Straight lines feel mechanical.
6. **Secondary action** — Smaller motions riding along with the primary (a logo lockup that wiggles as it lands; UI elements that settle differently).

### Beat structure for short product films (15-30s)

1. **Hook (0-2s)** — Bold motion or visual. Camera move + brand element.
2. **Reveal (2-6s)** — Product appears. Anticipation + arrival with overshoot.
3. **Demonstration (6-20s)** — Sequenced feature reveals. Standard delays, expressive easing on hero moments.
4. **Logo / CTA (20-30s)** — Logo lands with weight. Slow ease, settle with sheen or wipe.

## Brand identity animation

### Logo

- **Splash** — 100-150 frames at 30fps. Fade up + slight scale (95→100%). Hold 30+ frames. Fade out.
- **Zoom up** — Scale from 0%; Expressive ease. 30-45 frames. Subtle squash on landing.
- **Zoom sheen** — After zoom, a light sheen sweeps across (15-frame linear).
- **Wipe** — Vertical or horizontal mask wipe. 18-24 frames, Easy ease.

### Icons

| Icon motion | Frames @30fps | Easing | Notes |
|---|---|---|---|
| Change in state (heart fill, bookmark) | 6-9f | Easy | Source/dest at same anchor |
| Edge horizontal (nav arrows) | 12-18f | Easy | Hint motion direction |
| Animating arrows (continuous) | 24-30f loop | Linear | Loopable cycle |
| Add-to-cart bounce | 15f total | Exit | Scale 100→120→100 with overshoot |
| Favourite tap | 12f | Exit | Scale + color shift |

### Typography animation

- **Line by line** — 100ms (3f) delay per line. Easy ease. Slide-up from below or fade.
- **Highlighted text** — Word-by-word reveal with colored highlight wipe. 6f per word. Linear wipe, Easy ease text.
- **Wipe to right / left** — Mask reveal from edge. Easy ease. 18-24f short text, longer for long lines.
- **Type wipe** — Whole-line reveal. 12-18f.

## After Effects implementation specifics

### Speed Graph workflow

1. Set keyframes with default Linear interpolation
2. Select keyframes → F9 (Easy Ease) for the 33% baseline
3. Open Speed Graph (graph icon next to keyframes in timeline)
4. Drag handles to hit influence/velocity targets
5. For exact bezier values, use Flow plugin (paste `0.42, 0, 0.58, 1` style values)

### Naming convention

- Top-level comp: `MAIN_30s_v01`
- Sub-comps: `[role]_[content]_v01` — e.g., `card_features_v01`
- Nulls: `CTRL_*` for control rigs, `NULL_*` for parents
- Effects: leave default names except for shared expressions (rename to `LINK_*`)

### Useful plugins

- **Flow** — Edit easing curves, paste bezier values
- **EaseCopy** — Copy easing between properties
- **AEUX** — Figma → AE bridge
- **Bodymovin / Lottie** — Mobile JSON animation export
- **Motion (mt. Mograph)** — Inertia, anchor offsets, layer distribution

## Quick decision tree

When starting a new motion:

1. **What's changing?** State / position / size / opacity / multiple → Pick transition type
2. **What size is the change?** Small / medium / large → Pick duration row
3. **What's the priority?** Background / supporting / hero → Pick Quick / Standard / Slow
4. **What's the personality?** Calm / energetic / playful → Pick Easy / Expressive / Exit-Enter
5. **Is it part of a sequence?** Yes → Add delay (Tight / Standard / Emphasized)
6. **Anything that should follow through?** Yes → Add overshoot/wobble expression

## Output — Motion spec sheet

When asked to spec a motion, output this format:

```markdown
## Motion spec: [Component / Scene name]

**Trigger:** [What initiates the motion]
**Duration:** [ms] / [frames @ 30fps]
**Easing:** [Name] — bezier `[x1, y1, x2, y2]`
**Transition type:** [From the transitions table]
**Properties animated:** [Position / Scale / Opacity / Mask / etc.]

### Keyframes
| Time | Property | Value | Easing |
|---|---|---|---|
| 0f | [prop] | [value] | — |
| Xf | [prop] | [value] | [ease] |

### Sequence (if multi-element)
| Layer | Delay | Notes |
|---|---|---|
| [layer 1] | 0f | Base UI |
| [layer 2] | 3f | Standard delay |
| [layer 3] | 5f | Emphasized hero |

### Open questions
- [Anything that needs designer input]
```

## Output — Component recipe

```markdown
## Recipe: [Component name]

**Easing:** [Name + bezier]
**Duration:** [Quick / Standard / Slow] — [ms] / [frames]
**Transition:** [Type]
**Direction:** [If applicable: from-below, from-anchor, etc.]

### Setup
1. [Step]
2. [Step]
3. [Step]

### Don'ts
- [Anti-pattern]
```

## Tips

1. **Default to Easy ease + Standard duration.** Deviate when there's a reason.
2. **Stack motion principles.** Easing × duration × delay × transition shouldn't be picked independently — they have to feel like one decision.
3. **Test at 50% speed.** If it doesn't read at half speed, the easing is wrong.
4. **Test at 200% speed.** If it feels jittery, the duration is too short.
5. **Use Time Remap on a master comp** to globally retune timing without re-keyframing.
6. **Spec in frames for film/AE handoff, ms for prototype handoff.**

## Open decisions for Cloaked

This v1 is a draft to test the system. Refine over time:

- Should hero/key brand moments use a 6th custom Cloaked signature curve (e.g., something with a unique tail)?
- 30fps is assumed throughout — should we standardize on 24 (film) or 60 (high-refresh UI) for certain output types?
- Logo system needs Cloaked-specific lockup spec (pending brand guidelines).
- Define Cloaked-specific anticipation/overshoot defaults.
