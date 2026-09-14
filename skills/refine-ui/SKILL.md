---
name: refine-ui
description: Polish an existing screen or component against DESIGN.md and the UI craft catalogs, fixing spacing, radii, elevation, icons, motion and states in place.
disable-model-invocation: true
---

# Refine UI

A polish pass over a screen that already works. It fixes what makes the interface feel off, in the project's own idiom, without changing what the screen does.

1. Resolve the target: the path or route the user named, else the uncommitted UI changes. State it.
2. Read `DESIGN.md`. Every fix uses its tokens; a value not in the system is either added to `DESIGN.md` first or not used.
3. Call the Skill tool three times, for "anti-slop", "better-ui" and "emil-design-eng". Walk the target against all three catalogs, slowly: every state the component defines (hover, focus, active, loading, empty, error), motion replayed at 10% speed through the project's `verify` runtime loop when one exists.
4. Fix in place, cheapest fix first: delete, use the platform, reuse a token, correct the value, add. Keep the diff to polish; a behaviour change is a finding to report, not a change to make.
5. Report one table, grouped by principle, ordered by severity:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

Mark what could not be verified. If a fix settled a rule the system lacked, add it to `DESIGN.md`'s Decisions log.
