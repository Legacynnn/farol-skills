# Docs

The project's memory, written for humans and agents alike. Every doc below has one owner, fixed sections, and an **Update triggers** block that says when it changes. `sync-docs` walks these triggers after every spec, ticket, or decision; `add-doc` registers a new one.

Read order for a new session: `agents/README.md` first, then whatever the task names.

## Registry

| Doc | Purpose | Written by | Changes when |
| --- | --- | --- | --- |
| [agents/](./agents/README.md) | how agents navigate and work here | `setup-farol-skills`, `codebase-explore` | stack, layout, tracker or flow changes |
| [product/vision.md](./product/vision.md) | why this exists, for whom, what we will not do | humans, `grill-me` | positioning or audience shifts |
| [product/prd.md](./product/prd.md) | the product as a set of capabilities with status and measures | `to-spec`, `sync-docs` | a spec is published or shipped |
| [product/roadmap.md](./product/roadmap.md) | now / next / later, each item pointing at its spec | `to-spec`, `sync-docs` | a spec is created, started, shipped or dropped |
| [../DESIGN.md](../DESIGN.md) | the design system: tokens, components, motion, copy voice, bans, floor | `setup-farol-skills`, `shape-ui`, `finish-screen` | a design rule is settled |
| [design/brand.md](./design/brand.md) | identity beyond the UI: name, story, voice, marks, imagery | humans | brand decisions |
| [design/screens.md](./design/screens.md) | inventory of every screen with purpose, states, status, spec | `shape-ui`, `finish-screen`, `sync-docs` | a screen is planned, built or changed |
| [architecture/overview.md](./architecture/overview.md) | system shape: contexts, containers, data flow, boundaries, cross-cutting rules | `grill-me`, `to-spec`, `sync-docs` | a module, integration or boundary changes |
| [adr/](./adr/) | hard-to-reverse decisions, one file each | `domain-modeling` | a real trade-off is made |
| [../CONTEXT.md](../CONTEXT.md) | domain glossary | `domain-modeling` | a term is resolved |

Add a row for every doc you add. A doc not in this table does not exist to an agent.

## Conventions

- Frontmatter on every doc: `status` (`draft | living | frozen`), `updated` (ISO date), `owner` (a role or a skill).
- Sections are fixed; empty ones stay with `_none yet_` rather than being deleted, so a reader learns the shape.
- Facts point at their source: a spec path, an issue id, an ADR number, a commit. A claim with no pointer is a guess.
- Short beats complete. A doc grows by replacing lines, not by appending.
- Scratch (`.scratch/`) is where things are worked out; `docs/` is where what was decided lives. Nothing moves from scratch to docs without a decision behind it.
