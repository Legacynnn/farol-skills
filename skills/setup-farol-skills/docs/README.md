# Docs

The project's memory, for humans and agents alike. Each doc has fixed sections and one owner: the skill or role that writes it as part of doing its job. There is no separate "update the docs" step; the actor writes.

Read order for a new session: `agents/README.md` first, then whatever the task names.

## Registry

| Doc | What | Written by | When |
| --- | --- | --- | --- |
| [agents/](./agents/README.md) | how agents navigate and work here | `setup-farol-skills`, `codebase-explore` | stack, layout, tracker or flow changes |
| [product/vision.md](./product/vision.md) | why this exists, for whom, what we will not do | humans, `grill-me` | positioning or audience shifts |
| [product/prd.md](./product/prd.md) | capabilities per journey with status and spec pointer | `to-spec`, `to-tickets`, `implement` | a spec is published, started, shipped |
| [product/roadmap.md](./product/roadmap.md) | now / next / later / shipped / dropped | `to-spec`, `to-tickets`, `implement` | same events |
| [../DESIGN.md](../DESIGN.md) | design system: tokens, components, motion, copy, bans, floor | `setup-farol-skills`, `shape-ui`, `finish-screen` | a design rule is settled |
| [design/brand.md](./design/brand.md) | identity beyond the UI | humans | brand decisions |
| [design/screens.md](./design/screens.md) | every screen: purpose, states, status, spec | `shape-ui`, `prototype`, `finish-screen` | a screen is planned, prototyped, finished |
| [architecture/overview.md](./architecture/overview.md) | contexts, containers, data, request paths, boundaries, debt | `to-spec`, `domain-modeling`, `codebase-explore` | a module, integration, boundary or ADR changes |
| [adr/](./adr/) | hard-to-reverse decisions | `domain-modeling` | a real trade-off is made |
| [../CONTEXT.md](../CONTEXT.md) | domain glossary | `domain-modeling` | a term is resolved |

## Adding a doc

Copy [`_template.md`](./_template.md) into the folder it belongs to, fill the purpose paragraph and three to six sections, name the owner in the frontmatter, add a row above. A doc with no row does not exist to an agent; a doc with no owner rots.

## Conventions

- Frontmatter: `status` (`draft | living | frozen`), `updated` (ISO date), `owner`.
- Sections are fixed; an empty one reads `_none yet_` so the shape stays visible.
- Every fact points at its source: a spec, an issue, an ADR, a commit. Sources go under **Sources**.
- Docs grow by replacing lines. `.scratch/` is where things are worked out; `docs/` is what was decided.
