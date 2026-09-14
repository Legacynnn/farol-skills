# Issue tracker: Local markdown

Specs and tickets live as markdown in `.scratch/`. Scratch is committed unless the repo says otherwise.

## Layout

```
.scratch/
├── specs/<feature-slug>/
│   ├── spec.md
│   └── tickets/
│       ├── 01-<slug>.md
│       └── 02-<slug>.md
├── explorations/<topic>.md      ← codebase-explore and github-explore notes
└── prototypes/<name>/           ← logic prototypes (single HTML files)
```

## Conventions

- One feature per directory under `specs/`. The spec is `spec.md`.
- Tickets: one file each under `tickets/`, numbered from `01` in dependency order. Never one combined file.
- `Status:` line near the top of each ticket: `ready` | `in-progress` | `done` | `blocked`.
- `Blocked by:` line lists ticket numbers.
- Comments and session notes append under `## Log` at the bottom.

## Publish a spec

Write `.scratch/specs/<slug>/spec.md`.

## Publish tickets

Write `.scratch/specs/<slug>/tickets/NN-<slug>.md` per ticket.

## Fetch a ticket

Read the file at the path or number the user gives. With only a number, search `.scratch/specs/*/tickets/NN-*.md`.

## Frontier

Tickets whose `Blocked by` entries are all `done` and whose status is `ready`. Lowest number first.
