---
status: living
updated: <YYYY-MM-DD>
owner: to-spec, to-tickets, implement
---

# Product requirements

The product as a set of **capabilities**: what a user can do, grouped by journey, each with a status and a pointer to the spec that defines it. Detail lives in the specs; this doc is the map of them.

## Journeys

One section per top-level journey from `vision.md` Users. Under each, one row per capability.

### <Journey name>

<One line: who, from where, to what outcome.>

| Capability | Status | Spec | Measure |
| --- | --- | --- | --- |
| <user can ...> | `idea | specced | building | shipped | dropped` | <path or id> | <how success is read> |

## Cross-cutting requirements

Rules that apply to every capability: performance budgets, accessibility floor (see `DESIGN.md`), platforms, offline, privacy, i18n.

- <rule> (source: <ADR or spec>)

## Open problems

Problems from `vision.md` with no capability yet.

- <problem> → <what is blocking a spec>

## Sources

_none yet_
