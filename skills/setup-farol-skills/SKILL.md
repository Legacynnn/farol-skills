---
name: setup-farol-skills
description: "Configure this repo for farol-skills: issue tracker, agent navigation docs, DESIGN.md, domain doc layout. Run once per repo before the other skills."
disable-model-invocation: true
---

# Setup farol-skills

Scaffold the per-repo files every other farol skill reads. Prompt-driven, not a script: explore, present, confirm, write.

The output is the **agent docs**, the set of files an agent reads before it asks you anything:

| File | Owner | Purpose |
| --- | --- | --- |
| `docs/agents/README.md` | this skill | index of the agent docs and the order to read them |
| `docs/agents/issue-tracker.md` | this skill | where specs and tickets live and how to read/write them |
| `docs/agents/navigation.md` | this skill, then anyone | codebase map: entry points, key dirs, commands, conventions |
| `docs/agents/workflow.md` | this skill | the farol flow, phase boundaries, context hygiene |
| `docs/agents/domain.md` | this skill | how to consume `CONTEXT.md` and ADRs |
| `DESIGN.md` | this skill seeds, `shape-ui` and humans maintain | design system doc: audience, tone, tokens, components, motion, copy voice. **Required** for every UI skill |
| `docs/README.md` | this skill, humans | registry of every project doc: what, who writes it, when |
| `docs/product/{vision,prd,roadmap}.md` | humans, `to-spec`, `to-tickets`, `implement` | why, what capabilities, what order |
| `docs/design/{brand,screens}.md` | humans, `shape-ui`, `prototype`, `finish-screen` | identity beyond UI; screen inventory with states and status |
| `docs/architecture/overview.md` | `to-spec`, `domain-modeling`, `codebase-explore` | contexts, containers, data, request paths, boundaries, debt |
| `CONTEXT.md` | `domain-modeling`, lazily | domain glossary |
| `docs/adr/` | `domain-modeling`, lazily | decisions |

## Process

### 1. Explore

Read what exists before assuming anything:

- `git remote -v`: GitHub? GitLab? none?
- `CLAUDE.md`, `AGENTS.md` at root: which exists, is there already an `## Agent skills` block?
- `docs/agents/`, `DESIGN.md`, `.impeccable.md`, `CONTEXT.md`, `docs/adr/`, `.scratch/`
- Linear signals: `.linear` config, Linear MCP available, issue keys like `ABC-123` in git log
- Stack: package manager, framework, styling system (Tailwind, CSS modules, vanilla), component library, motion library, test runner, task runner scripts
- Layout: monorepo signals (`pnpm-workspace.yaml`, `workspaces`, populated `packages/*`)
- Existing design tokens: `tailwind.config.*`, `globals.css`, `theme.*`, a `tokens` dir, Storybook

### 2. Present and ask

Summarise findings. Then take sections in order, one answer each, leading with the recommended answer so the user can accept in a word.

**Section A: Issue tracker.** Where specs and tickets live. Propose from evidence:

- **Linear** when Linear signals were found (uses the Linear MCP tools)
- **GitHub** when the remote is GitHub and no Linear signal (uses `gh`)
- **Local markdown** otherwise: `.scratch/specs/<slug>/` in this repo

Ask which team / project key when Linear. Record in `docs/agents/issue-tracker.md` from the matching template in this folder.

**Section B: DESIGN.md.** If `DESIGN.md` exists, keep it and skip. If `.impeccable.md` exists, promote its Design Context into `DESIGN.md` Product. Otherwise seed `DESIGN.md` from [design.md](./design.md), pre-filling every field exploration can answer (tokens, stack, component library, motion library, fonts) and asking only the fields code cannot answer: audience, jobs to be done, tone in three concrete words, references and anti-references, theme context (when, where, by whom). Five questions, not twenty. Fonts and palette that are still reflex defaults get flagged as `<decide via anti-slop>` rather than copied in.

Always write `.impeccable.md` as a mirror so impeccable's own commands read the same context: a `## Design Context` section with Users, Brand Personality, Aesthetic Direction, Design Principles, copied from `DESIGN.md` Product, plus the line `Source of truth: DESIGN.md`.

**Section C: Navigation.** Draft `docs/agents/navigation.md` from [navigation.md](./navigation.md) with what exploration found. Show it; the user corrects, not authors.

**Section D: Domain docs.** Default single-context (`CONTEXT.md` at root, `docs/adr/`). Offer multi-context only on monorepo signals.

**Section E: Project docs.** Scaffold the full layout from [docs/](./docs/) by default: `README.md` (registry), `_template.md`, `product/vision.md`, `product/prd.md`, `product/roadmap.md`, `design/brand.md`, `design/screens.md`, `architecture/overview.md`. Pre-fill from exploration: containers and request paths from the code, screens from the routes, the one-line from the README, users and tone from Section B answers (the same three questions feed `DESIGN.md` Product and `vision.md` Users, so ask once). Every section you cannot fill keeps `_none yet_`. Existing docs with the same names are kept and only the registry row is added. Ask one question: skip any of these? A repo that is a library or a CLI usually drops `design/`.

### 3. Confirm and write

Show the drafts of every file and the `## Agent skills` block. Let the user edit. Then write.

**Pick the instructions file:** edit `CLAUDE.md` if it exists, else `AGENTS.md`, else ask which to create. Never create the second when the first exists. If an `## Agent skills` block exists, update in place.

The block:

```markdown
## Agent skills

Read `docs/agents/README.md` before exploring or asking questions. It indexes the agent docs.

- Issue tracker: [one-liner]. See `docs/agents/issue-tracker.md`.
- Navigation: `docs/agents/navigation.md`.
- Workflow: `docs/agents/workflow.md`.
- Design system: `DESIGN.md`. Required reading before any UI work.
- Domain: [single-context | multi-context]. See `docs/agents/domain.md`.
- Project docs: `docs/README.md` is the registry; each doc names the skill that writes it. To add one, copy `docs/_template.md` and add a row.
```

Write from the templates in this folder:

- [README.md](./README.md): the index
- [issue-tracker-linear.md](./issue-tracker-linear.md), [issue-tracker-github.md](./issue-tracker-github.md), [issue-tracker-local.md](./issue-tracker-local.md)
- [navigation.md](./navigation.md)
- [workflow.md](./workflow.md)
- [domain.md](./domain.md)
- [design.md](./design.md) as `DESIGN.md` at the repo root
- [docs/](./docs/): the project docs layout, folder for folder, each file dated and marked `draft` until a human edits it

### 4. Done

Tell the user to run `/setup-verify` next, so the flow skills can verify their work in this project. Say which skills now read these files. Every doc under `docs/` and `DESIGN.md` is living: `codebase-explore` proposes navigation edits when it finds the map stale, `shape-ui` and `finish-screen` update `DESIGN.md` when a decision lands. Re-run this skill only to switch tracker or restart.
