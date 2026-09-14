# Workflow

The farol flow. Skills are steps; the docs in this folder are what every step reads first.

## Main flow: idea to shipped

1. **Explore** (any combination): `/codebase-explore` for the current repo, `/github-explore <url>` for an open-source repo. Both leave notes in `.scratch/explorations/`.
2. **Sharpen**: `/grill-me`. Reads the agent docs, `DESIGN.md` and `CONTEXT.md` first and never asks what they already answer. Updates `CONTEXT.md` and ADRs as terms and decisions land.
3. **Prototype when talk is not enough**: `/prototype`. Logic question: one HTML file. UI question: variants behind a picker, styled from `DESIGN.md`. Verdict flows back into the spec.
4. **Spec**: `/to-spec`. Problem, journeys, requirements, decisions. Published to the tracker.
5. **Tickets**: `/to-tickets`. Small vertical slices, one session each, blocking edges declared.
6. **Build**: `/implement <ticket>` per ticket, fresh context per ticket.
7. **Finish UI**: `/finish-screen` on any screen a ticket produced; `/review-ui` before merge.

## UI side-flow

- `/shape-ui` before code, when the UX itself is undecided. Updates `DESIGN.md`.
- `/refine-ui`, `/fix-copy`, `/mobile-first` are single-purpose passes over an existing screen.
- `better-ui` and `emil-design-eng` are the rule catalogs every UI skill loads.

## Context hygiene

Keep steps 1 to 5 in one context window. `/implement` starts fresh per ticket. Compact at a phase boundary, never mid-phase.
