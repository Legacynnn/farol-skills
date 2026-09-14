---
name: mobile-first
description: Refactor a screen to a mobile-first layout that grows through the DESIGN.md breakpoints, with touch targets, safe areas and no horizontal scroll at 320px.
disable-model-invocation: true
---

# Mobile first

Rebuild the layout of a screen from the narrowest width up. The 320px rendering is the base case; larger breakpoints only add.

1. Resolve the target and read `DESIGN.md` (Foundations: breakpoints, spacing; Patterns: shells, density).
2. Audit at 320px, then at each `DESIGN.md` breakpoint, in a browser when available: horizontal overflow, clipped or overlapping content, tap targets under 44px, fixed widths, hover-only affordances, content reachable only by hover or wide viewport, `100vh` on mobile browsers, missing safe-area insets.
3. Refactor, keeping behaviour identical:
   - Base styles are the mobile layout; breakpoints are `min-width` only. Remove `max-width` media queries.
   - Single column by default; grids and side-by-side arrive at the breakpoint that fits them.
   - Fluid units and `max-width: 100%` on images and aspect boxes; no `min-width` wider than the viewport.
   - Touch targets at least 44px with spacing between them; hover states gated by `@media (hover: hover) and (pointer: fine)`.
   - Sticky and fixed chrome respects `env(safe-area-inset-*)`; use `dvh` over `vh`.
   - Tables, code and diagrams get their own `overflow-x: auto` container; the page never scrolls sideways.
   - Text wraps: `overflow-wrap: anywhere` on user content, `text-wrap: balance` on headings.
4. Call the Skill tool with "better-ui" for hit areas and motion under touch. Verify again at every breakpoint.
5. Report `| Breakpoint | Before | After | Why |` and note what could not be verified. Record any new breakpoint rule in `DESIGN.md`.
