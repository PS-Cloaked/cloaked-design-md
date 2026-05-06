# Cloaked — Tokens

## Typography
<!-- TODO: Fill from Figma Foundation page -->

## Color

Color primitives from the Figma Variables "Colors" collection.
Source of truth: Figma. These are referenced by semantic tokens
in the Theme collection.

### Primitives

| Name | Hex |
| ---- | --- |
| White | #FFFFFF |
| Grey-01 | #F3F1ED |
| Grey-02 | #DCD8CF |
| Grey-03 | #84827E |
| Grey-04 | #1B1B18 |
| Grey-05 | #141410 |
| Black | #0B0B0A |
| Brand | #FF550C |
| Green-01 | #008924 |
| Green-02 | #008924 |
| Red-01 | #B83100 |
| Red-02 | #B83100 |
| White-05 | #FFFFFF |
| White-15 | #FFFFFF |
| Black-05 | #0B0B0A |
| Black-15 | #0B0B0A |

### Notes
- The numeric suffix on `White-05`, `White-15`, `Black-05`, and
  `Black-15` denotes alpha (5% and 15%), not a hex variant — they
  share the base `White` / `Black` hex with reduced opacity.
- `Green-02` and `Red-02` follow the same convention: same hex as
  their `-01` counterpart at 10% alpha, intended for tinted
  backgrounds paired with the solid `-01` foreground.
- Hex alone is lossy for these tokens; consumers that need the
  alpha channel should read from the Figma export rather than
  this table.

## Theme
<!-- TODO: Fill from Figma Foundation page -->

## Grid & Spacing
<!-- TODO: Fill from Figma Foundation page -->
