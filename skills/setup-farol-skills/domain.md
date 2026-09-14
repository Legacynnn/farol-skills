# Domain docs

How skills consume this repo's domain documentation.

## Before exploring, read

- `CONTEXT.md` at the repo root, or `CONTEXT-MAP.md` when multi-context (it points at one `CONTEXT.md` per context).
- `docs/adr/`: ADRs touching the area you are about to work in.

If a file is missing, proceed silently. `domain-modeling` (via `/grill-me`) creates them lazily.

## Use the glossary's vocabulary

When output names a domain concept (ticket title, test name, component name), use the term as `CONTEXT.md` defines it. Never drift to a synonym the glossary lists under `_Avoid_`. A concept missing from the glossary is a signal: either invented language or a real gap to note for `domain-modeling`.

## Flag ADR conflicts

Output that contradicts an ADR says so explicitly instead of silently overriding:

> _Contradicts ADR-0007 (event-sourced orders), worth reopening because..._

## Layout

Single context (default): `CONTEXT.md` + `docs/adr/` at root.
Multi context: `CONTEXT-MAP.md` at root, `src/<context>/CONTEXT.md` and `src/<context>/docs/adr/` per context, `docs/adr/` for system-wide decisions.
