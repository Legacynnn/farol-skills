---
status: living
updated: <YYYY-MM-DD>
owner: to-spec, domain-modeling, codebase-explore
---

# Architecture

The shape of the system in one read. Detail lives in the code and `docs/agents/navigation.md`; decisions live in `docs/adr/`. This doc is the map between them.

## System context

What the system is, who and what talks to it, one paragraph. Then the external systems, one line each with the direction of the dependency.

- **<External system>**: <we call it | it calls us>, for <purpose>, contract at <path or url>

## Contexts

One row per bounded context (single-context repos have one row). Matches `CONTEXT.md` / `CONTEXT-MAP.md`.

| Context | Owns | Lives at | Talks to |
| --- | --- | --- | --- |

## Containers

The deployable pieces: apps, services, workers, databases, queues.

| Container | Role | Runtime | Scales by | Talks to |
| --- | --- | --- | --- | --- |

## Data

The core entities and who owns each; the store per container; how data moves between containers (sync call, event, batch). Schema detail stays in the code.

- **<Entity>**: owned by <context>, stored in <store>, referenced elsewhere by id only

## Request paths

The two or three paths that matter most, each as one line of hops: `browser → app router → service → db`.

1. **<path name>**: <hops>

## Cross-cutting

Auth, authorisation, errors, observability, background jobs, feature flags, i18n: one line each saying the mechanism and where it lives.

- **Auth**: <mechanism>, at <path>

## Boundaries and rules

The invariants a change must not break, each pointing at its ADR.

- <rule> (ADR-<nnnn>)

## Known debt

What is wrong, why it is still there, what would fix it.

- <debt>: <why>, fix: <what>, tracked at <issue>

## Sources

_none yet_
