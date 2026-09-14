---
name: finish-screen
description: Finish a screen to production standard against DESIGN.md (states, responsiveness, polish, motion, copy, accessibility floor). Use when a prototype variant wins, when implement produces UI, or when the user asks to finish, productionise, or ship a screen.
---

# Finish screen

The bridge from "it works" or "we picked this variant" to "this ships". Prototype code was written under prototype rules; this rewrites it properly.

1. Resolve the target: the winning variant, the route, or the component the user names. Read the ticket or spec it belongs to, `DESIGN.md`, `CONTEXT.md`, `docs/agents/navigation.md`.
2. Rebuild in the project's idiom: library components over one-offs, tokens over literals, the folder and naming conventions `navigation.md` records. Delete prototype-only scaffolding (switcher, stubs, `?variant=`).
3. Ship every state `DESIGN.md` requires: loading (skeleton or spinner matching the system), empty (what belongs here plus primary action), error (what happened and how to recover), narrow width (320px holds). Long content, missing images, i18n-length strings, and slow networks each have a defined rendering.
4. Run the passes in order, one Skill tool call each: "anti-slop" (bans, font, colour, structure), "mobile-first" (320px up), "better-ui" and "emil-design-eng" (polish and motion), "fix-copy" (every string).
5. Clear the floor `DESIGN.md` names under Patterns, every item.
6. Verify in a browser when available: each state, each breakpoint, keyboard-only pass, motion at 10% speed. Report what was verified and what was not.
7. Log the decisions the finish settled in `DESIGN.md`, then call the Skill tool with "sync-docs" for the event "screen finished". Hand back to the ticket: criteria ticked, ready for `/review-ui`.
