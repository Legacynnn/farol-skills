---
name: shape-ui
description: Plan the UX and UI of a feature before code, against DESIGN.md, producing a short design brief and updating DESIGN.md with any rule the plan settles.
disable-model-invocation: true
---

# Shape UI

Decide what a screen or flow is before anyone builds it. Output is a **design brief** the spec and prototype consume, never code.

1. Read `DESIGN.md`, `CONTEXT.md`, `docs/agents/navigation.md`. If `DESIGN.md` is missing, stop and tell the user to run `/setup-farol-skills`; shaping without it produces generic UI.
2. Call the Skill tool with "grilling", scoped to the screen: who arrives here and from where, the one primary action, what they must see first, the states (loading, empty, error, narrow width), what is destructive and how it is confirmed, what the copy voice says here. `DESIGN.md` already answers most of it; only the open branches get asked.
3. Call the Skill tool with "anti-slop" and run its font, colour and structure procedures for anything `DESIGN.md` leaves undecided; then "emil-design-eng" for the motion decisions the brief must fix: what animates, how often it is seen, what stays instant.
4. Write the brief to `.scratch/specs/<slug>/design-brief.md` (or the tracker issue when the spec already lives there):

```md
# <Screen or flow>

**For**: <actor, context, device>. **Arrives from**: <entry>. **Leaves to**: <exit>.
**Primary action**: <one>. **Secondary**: <few>.
**Hierarchy**: what is seen first, second, third.
**Layout**: which `DESIGN.md` shell and patterns; mobile-first sketch in words, then how it grows at each breakpoint.
**Components**: reused from the library; new ones named and justified.
**States**: loading, empty, error, narrow width, each in one line.
**Motion**: what moves, why, exact durations and easings from `DESIGN.md`; what is instant.
**Copy**: labels and messages in the `DESIGN.md` voice.
**Open for prototype**: the one or two questions only a `/prototype` can settle, each with the axis to diverge on.
```

5. Append every settled rule as one dated line in `DESIGN.md`'s Decisions log. The brief is disposable; `DESIGN.md` is not.
