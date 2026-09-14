---
name: to-spec
description: "Turn the current conversation into a spec (problem, user journeys, requirements, decisions) and publish it to the project's issue tracker. No interview: synthesis of what is already known."
disable-model-invocation: true
---

# To spec

Take the conversation, the explorations in `.scratch/explorations/`, any prototype verdict, and produce one spec. Do NOT interview the user again; synthesise. A gap you cannot fill from context is listed under **Open questions**, not asked.

`docs/agents/issue-tracker.md` says where specs go. If missing, tell the user to run `/setup-farol-skills`.

## Process

1. Read `docs/agents/README.md` and what it indexes if not already in context, plus `docs/product/vision.md` and `docs/architecture/overview.md`; the Problem traces to the first, the implementation decisions respect the second. Use `CONTEXT.md` vocabulary throughout. Respect ADRs; contradict one only explicitly.
2. Sketch the seams you will test the feature at. Prefer existing seams, at the highest point possible; ideal count is one. Confirm the seams with the user in one message.
3. Write the spec from the template. Publish per the tracker doc. Link explorations and the prototype branch by path or URL rather than pasting them in.
4. Record it: a capability row per journey in `docs/product/prd.md` (status `specced`, spec pointer), an item under Next in `docs/product/roadmap.md`, and any new module, integration or entity in `docs/architecture/overview.md`, each with the spec as source.

<spec-template>

# <Feature name>

## Problem

The problem at the product level, from the user's perspective: who is stuck, on what, and what it costs them today. No solution language here.

## Outcome

What is true for the user once this ships, in two or three sentences.

## User journeys

One numbered journey per actor and goal, written as the end-to-end path through the product:

1. **<Actor> <does goal>**: starts at <entry>, sees <state>, does <action>, ends with <result>. Edge: <what happens when it goes wrong>.

Cover the happy path, the empty and error states, and the narrow-width path for any screen. This list is long and complete; it is what tickets and tests derive from.

## Requirements

The things the solution must do, grouped by journey, each one testable. Include the states `DESIGN.md` requires for every screen. Mark the few that are `MUST` vs `SHOULD`.

## Design

The screens and components touched, the `DESIGN.md` patterns they use, the prototype verdict (which variant, why, link to the `prototype/<name>` branch). Any rule this feature settled is already a line in `DESIGN.md`'s Decisions log; reference it.

## Implementation decisions

Modules built or modified and their interfaces, schema changes, API contracts, architectural choices, developer clarifications. No file paths, no code, except a prototype snippet that encodes a decision more precisely than prose (state table, reducer signature, type shape), trimmed to the decision-rich part and marked as from the prototype.

## Testing decisions

What a good test is here (external behaviour through the seams, never internals), which seams are under test, prior art in the codebase.

## Out of scope

Explicit no-s, so the next reader does not reopen them.

## Open questions

Anything the conversation left unsettled. Empty is the goal.

</spec-template>
