# DESIGN.md

The design system as an agent reads it. Every UI skill loads this before touching a screen. Fields exploration can fill are pre-filled; the rest come from the humans. Keep every value exact: a token name, a pixel value, a curve.

## Product

- **Audience**: `<who, in what context, on what device most of the time>`
- **Jobs**: `<the two or three things users come here to do>`
- **Tone**: `<three adjectives, e.g. calm, precise, warm>`; never `<what it must not feel like>`
- **References**: `<products or sites whose feel we want, with the one thing to take from each>`

## Foundations

- **Type**: `<font family>` for UI, `<font family>` for display; scale `<steps>`; body `<size>/<line-height>`; tabular numbers on data
- **Color**: tokens at `<path>`; semantic roles: `bg`, `surface`, `border`, `fg`, `muted`, `accent`, `danger`, `success`; dark mode via `<class | media>`
- **Spacing**: `<4px grid | 8px grid>`; section gap `<value>`; card padding `<value>`
- **Radius**: `<sm/md/lg values>`; nested surfaces follow concentric radius (outer = inner + padding)
- **Elevation**: shadows for depth, borders for structure; shadow tokens `<names>`
- **Breakpoints**: mobile first; `<sm/md/lg values>`; minimum supported width 320px

## Components

- **Library**: `<shadcn | base-ui | custom>` at `<path>`; add here, never inline one-offs
- **Primitives to reuse**: `<Button, Input, Card, Sheet, Dialog, Toast...>` with paths
- **Icons**: `<lucide | ...>`, stroke `<1.5px beside 400 text, 2px beside 600>`, outline default, fill for active

## Motion

- **Easing**: `--ease-out: cubic-bezier(0.23, 1, 0.32, 1)`; `--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1)`; never `ease-in` on UI
- **Duration**: press `100-160ms`, popovers `125-200ms`, dropdowns `150-250ms`, modals and drawers `200-500ms`; UI stays under `300ms`
- **Rules**: transform and opacity only; exits softer and faster than enters; no animation on keyboard-driven or 100+/day actions; `prefers-reduced-motion` honoured
- **Library**: `<motion | css only>`

## Copy

- **Voice**: `<sentence case, second person, no exclamation marks>`
- **Labels**: verbs on buttons (`Save changes`, not `Submit`); errors say what happened and how to recover
- **Empty states**: one line of what goes here plus the primary action

## Patterns

- **Layout shells**: `<app shell, marketing shell, auth shell>` at `<paths>`
- **Data density**: `<dense tables | airy cards>` by surface
- **States every screen ships with**: loading, empty, error, narrow width

## Decisions log

Append one line per settled design decision with the date. `shape-ui` and `finish-screen` write here.

- `2026-01-01`: `<decision>`
