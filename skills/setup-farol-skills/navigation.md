# Navigation

The codebase map for agents. Kept short and current; a stale line here costs every session. `codebase-explore` proposes edits when it finds drift.

## Stack

- Language / framework: `<...>`
- Package manager and task runner: `<pnpm | bun | ...>`; scripts in `package.json`
- Styling: `<Tailwind vX | CSS modules | ...>`; tokens at `<path>`
- Component library: `<shadcn | base-ui | ...>` at `<path>`
- Motion: `<motion | none>`
- Tests: `<vitest | ...>`; run one file with `<cmd>`
- Typecheck: `<cmd>`

## Entry points

- App entry: `<path>`
- Routing: `<convention, e.g. app/(routes)/...>`
- API / server: `<path>`
- DB / schema: `<path>`; migrations: `<cmd>`

## Where things live

| Concern | Path | Note |
| --- | --- | --- |
| UI components | `<path>` | |
| Feature modules | `<path>` | |
| Shared utils | `<path>` | |
| Config / env | `<path>` | |

## Conventions the code does not confess

- `<e.g. every route reads session via getSession(), never cookies() directly>`
- `<e.g. feature dirs own their queries; no cross-feature imports>`

## Run it

- Dev: `<cmd>` at `<url>`
- Prototype route convention: `<e.g. app/prototype/<name>/page.tsx>`, dev-only

## Gotchas

- `<the thing that bites every new session>`
