---
name: anti-slop
description: The AI-slop tells in generated UI and how to design past them, distilled from impeccable.style. Use when building or reviewing any screen, choosing fonts, colours, theme or layout, or when a UI reads as generic, templated, or "an AI made this".
---

# Anti-slop

**Slop** is the fingerprint of generated UI: the reflex choices every model makes when no one decides. This skill is the match-and-refuse list plus the procedures that replace each reflex with a decision. `DESIGN.md` holds the decisions once made; this is how they get made.

Deeper material, load on demand: [typography](reference/typography.md), [color and contrast](reference/color-and-contrast.md), [spatial design](reference/spatial-design.md), [interaction](reference/interaction-design.md), [responsive](reference/responsive-design.md), [UX writing](reference/ux-writing.md). Motion values live in `emil-design-eng`; polish values in `better-ui`.

## The slop test

Shown this screen and told "an AI made this", would someone believe it at once? If yes, it fails. A designed interface makes people ask "how was this made?".

## Absolute bans

Match and refuse. On sight, rewrite the element with a different structure, never a swap of the same idea:

| Ban | Pattern | Rewrite |
| --- | --- | --- |
| Side-stripe accent | `border-left`/`border-right` wider than 1px on cards, rows, callouts, alerts, any colour, any variable | full border, background tint, leading number or icon, or nothing |
| Gradient text | `background-clip: text` over any gradient | one solid colour; emphasis by weight or size |
| AI palette | cyan on dark, purple-to-blue gradients, neon accents on dark | a brand hue chosen from the brief, neutrals tinted toward it |
| Pure black or white | `#000`, `#fff` | tinted near-black and near-white |
| Everything in cards | cards inside cards, identical icon+heading+text card grids, hero-metric template (big number, small label, gradient accent) | flatten; vary structure; left-align |
| Decorative glass and glow | blur, glass cards, glow borders with no purpose | shadows for depth, borders for structure (`better-ui`) |
| Decorative sparklines | tiny charts that convey nothing | data with a reading, or no chart |
| Modal by default | a dialog where an inline, sheet, or page would do | progressive disclosure, inline edit, a route |
| Uniform spacing | the same padding everywhere, everything centred | rhythm: tight groups, generous separations, asymmetry on purpose |
| Icon-above-heading | a rounded icon tile above every heading | remove; let type carry hierarchy |

## Font procedure

Run before typing any font name. The reflex is "not Inter, so my second favourite", which is a new monoculture.

1. Write three concrete brand words from the brief ("warm, mechanical, opinionated"). Never "modern" or "elegant".
2. List the three fonts you would reach for. Reject every one on the reflex list: Inter, Roboto, Arial, Open Sans, system defaults, Fraunces, Newsreader, Lora, Crimson (any), Playfair Display, Cormorant (any), Syne, IBM Plex (any), Space Mono, Space Grotesk, DM Sans, DM Serif (any), Outfit, Plus Jakarta Sans, Instrument (any).
3. Browse a catalogue (Google Fonts, Pangram Pangram, Future Fonts, Klim, ABC Dinamo, Velvetyne) with the three words, looking for the font as a physical object: a shop sign, a terminal manual, a coat label. Reject the first thing that "looks designy".
4. Cross-check: elegant is not necessarily serif, technical is not necessarily sans or mono. If the pick matches the reflex pattern, return to 3.
5. Pair a distinctive display face with a refined body face. Scale of five steps at a ratio of at least 1.25; fluid `clamp()` on marketing headings, fixed `rem` in product UI; body measure 65 to 75ch.

Record the pair and the reason in `DESIGN.md` Foundations.

## Colour and theme procedure

1. Pick the brand hue from the brief, never from a "warm = friendly" formula.
2. Build in OKLCH. Tint every neutral toward the brand hue (chroma 0.005 to 0.01). Reduce chroma as lightness approaches white or black.
3. Weight 60/30/10: surface, secondary text and borders, accent. Accents work because they are rare.
4. Derive light or dark from when, where and by whom the product is used (a trading desk at night is dark; a patient portal on a phone is light). Both defaults are the reflex; the context decides.

Record hue, neutrals, theme and the reason in `DESIGN.md` Foundations.

## Structure procedure

1. Commit to one aesthetic direction in a phrase (brutally minimal, editorial, industrial, soft, luxury) and execute it with precision. Intentionality, not intensity.
2. Spacing on a 4pt scale with semantic tokens; `gap` over margins; vary spacing for hierarchy.
3. Container queries for components, viewport queries for page layout; `repeat(auto-fit, minmax(280px, 1fr))` for card content.
4. Empty states teach the interface. Every word earns its place; nothing restates what the user can see. Button hierarchy: one primary, the rest ghost or text.
5. Adapt for mobile; never amputate.

## In a review

Each ban found is one finding, `MEDIUM` by default, `HIGH` when it is systemic (a token, a shared component). Cite `path:line`, the pattern, the rewrite.
