---
name: ask-farol
description: Ask which farol skill or flow fits your situation. A router over the skills in this set.
disable-model-invocation: true
---

# Ask Farol

You don't remember every skill, so ask. A **flow** is a path through the skills. The agent docs (`docs/agents/`, `DESIGN.md`, `CONTEXT.md`) are what every step reads first, so the flow starts with `/setup-farol-skills` once per repo.

## Main flow: idea to shipped

1. **Explore**, in any combination, before or during the interview:
   - **`/codebase-explore`** answers a question about this repo with citations and leaves a note in `.scratch/explorations/`.
   - **`/github-explore <url>`** clones an open-source repo into a cache, explains how something works inside it, and leaves a note saying what transfers here.
2. **`/grill-me`** sharpens the idea by interview. It reads the docs first and never asks what they answer; terms go to `CONTEXT.md`, hard decisions to ADRs, design rules to `DESIGN.md`.
3. **Branch: does a question need a runnable answer?** → **`/prototype`**: a logic question gets one HTML file; a UI question gets variants behind a picker, styled from `DESIGN.md`. The verdict flows back into the thread.
4. **Branch: is the UX itself undecided?** → **`/shape-ui`** first, a brief per screen, before prototyping.
5. **`/to-spec`** turns the thread into a spec: problem, journeys, requirements, decisions. Published to the tracker.
6. **`/to-tickets`** splits it into session-sized vertical slices with blocking edges.
7. **`/implement <ticket>`** per ticket, fresh context each. It drives `tdd` at the agreed seams, loads the UI catalogs for any screen, closes with `code-review`, commits. **`/implement-spec`** (experimental) works the whole ticket graph instead: concurrent implementer subagents in worktrees, merged as the frontier moves, one PR.
8. **`/review-ui`** on the branch or PR before merge.

Keep steps 1 to 6 in one context window. Compact at a phase boundary, never mid-phase.

## UI passes, any time

Single-purpose passes over an existing screen. Each reads `DESIGN.md` and loads the catalogs.

- **`/refine-ui`**: polish (spacing, radii, elevation, icons, motion, states).
- **`fix-copy`**: every string in the product voice. Model-invoked, so "fix the wording" reaches it.
- **`mobile-first`**: rebuild the layout from 320px up. Model-invoked, so "make it responsive" reaches it.
- **`finish-screen`**: all of the above plus every state and the floor. Model-invoked: `implement` calls it on any screen a ticket produces; you call it on a prototype winner.

## Vocabulary underneath

Model-invoked references the skills above pull in. Reach for them directly when the words, not the process, are the problem.

- **`/grilling`**: the interview primitive.
- **`/domain-modeling`**: glossary and ADR discipline.
- **`/tdd`**: red-green at pre-agreed seams.
- **`/code-review`**: two-axis diff review, Standards and Spec, in parallel sub-agents.
- **`/anti-slop`**: the AI-slop bans and the font, colour, structure procedures that replace reflex choices (impeccable.style).
- **`/better-ui`**: exact values for radii, shadows, icons, enter/exit, performance (Jakub Krehel).
- **`/emil-design-eng`**: the animation decision framework, springs, gestures, review table (Emil Kowalski).

## Docs

The project docs under `docs/` (product vision, PRD, roadmap; brand, screens; architecture) are written by the flow skills as they go: the actor writes, there is no sync step. `docs/README.md` is the registry; copy `docs/_template.md` and add a row to extend it.

## Making skills

- **`/write-skill`**: write or review a skill, for this project or for farol-skills, applying `writing-for-agents`.
- **`/writing-for-agents`**: the reference for any document an agent consumes.

## Precondition

**`/setup-farol-skills`** once per repo: tracker (Linear, GitHub, or local `.scratch/`), `docs/agents/` navigation docs, `DESIGN.md`, the `docs/` layout. Then **`/setup-verify`** once per repo: it detects the stack and writes the project's **`verify`** skill, the loop every flow skill closes on (browser via Chrome MCP, simulator, emulator, Tauri MCP, Electron CDP, curl, golden files). Re-run when the stack changes.
