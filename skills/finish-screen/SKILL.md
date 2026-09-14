---
name: finish-screen
description: Take a prototype winner or a rough screen to production standard against DESIGN.md, with every state, copy, responsiveness, accessibility and motion done.
disable-model-invocation: true
---

# Finish screen

The bridge from "it works" or "we picked this variant" to "this ships". Prototype code was written under prototype rules; this rewrites it properly.

1. Resolve the target: the winning variant, the route, or the component the user names. Read the ticket or spec it belongs to, `DESIGN.md`, `CONTEXT.md`, `docs/agents/navigation.md`.
2. Rebuild in the project's idiom: library components over one-offs, tokens over literals, the folder and naming conventions `navigation.md` records. Delete prototype-only scaffolding (switcher, stubs, `?variant=`).
3. Ship every state `DESIGN.md` requires: loading (skeleton or spinner matching the system), empty (what belongs here plus primary action), error (what happened and how to recover), narrow width (320px holds). Long content, missing images, i18n-length strings, and slow networks each have a defined rendering.
4. Run the passes in order, each as the Skill tool call: "mobile-first" is user-invoked, so apply its rules directly here; then "better-ui", "emil-design-eng" for polish and motion; then apply the "fix-copy" rules to every string.
5. Accessibility floor, no exceptions: every control has an accessible name, keyboard reaches everything a pointer does, focus is visible, contrast passes, nothing rides on colour alone, `prefers-reduced-motion` honoured, destructive actions confirmed.
6. Verify in a browser when available: each state, each breakpoint, keyboard-only pass, motion at 10% speed. Report what was verified and what was not.
7. Log the decisions the finish settled in `DESIGN.md`. Hand back to the ticket: criteria ticked, ready for `/review-ui`.
