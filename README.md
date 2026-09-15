# farol-skills

One skill set for the whole loop: explore, grill, prototype, spec, tickets, build, verify, finish the screen. Every skill reads the repo's docs first (`docs/agents/`, `DESIGN.md`, `CONTEXT.md`, the project `verify` skill) so nothing documented gets asked twice, no UI gets built off-system, and nothing reports done without evidence.

Merged and adapted from [mattpocock/skills](https://github.com/mattpocock/skills), [jakubkrehel/skills](https://github.com/jakubkrehel/skills), [emilkowalski/skills](https://github.com/emilkowalski/skills) and [impeccable](https://impeccable.style). See [`NOTICE.md`](./NOTICE.md).

## Install

Claude Code plugin, read-only, updates with the repo:

```
/plugin marketplace add Legacynnn/farol-skills
/plugin install farol-skills@farol
```

Local symlinks for any harness (Claude Code and Codex), including `experimental/`, from a clone:

```bash
scripts/link-skills.sh
```

Then, once per repo:

```
/setup-farol-skills
/setup-verify
```

## The flow, end to end

Everything below runs in one context window until tickets exist; each ticket then gets a fresh one.

**0. Setup, once per repo.** `/setup-farol-skills` explores the repo, asks five questions (tracker, audience, jobs, tone, theme context) and writes the docs every other skill reads: `docs/agents/` (navigation, workflow, tracker, domain), `DESIGN.md`, and the project docs layout (product vision, PRD, roadmap; brand, screens; architecture). `/setup-verify` detects every surface (web, API, CLI, Electron, Tauri, Expo, native), runs each command once, proves a runtime probe per surface (Chrome MCP, simulator, emulator, Tauri MCP, CDP, curl), and writes `.claude/skills/verify/`: the loop every flow skill closes on.

**1. Explore.** `codebase-explore` answers "how does X work here" with `path:line` citations and leaves a note in `.scratch/explorations/`. `github-explore <url>` clones an open-source repo into a cache, traces the same way, and says what transfers to this stack and licence. Both feed the interview; neither edits source.

**2. Grill.** `/grill-me` runs the interview in rounds over the design tree. It reads the docs first and cites them instead of asking; facts are fetched by sub-agents, decisions are yours. Terms land in `CONTEXT.md`, hard trade-offs in `docs/adr/`, design rules in `DESIGN.md`. When the UX itself is undecided, `/shape-ui` runs a screen-scoped interview and writes a design brief plus the screen's row in `docs/design/screens.md`.

**3. Prototype when talk is not enough.** `prototype` builds throwaway code that answers one question. A logic question becomes one HTML file a non-developer can drive. A UI question becomes three to five variants that disagree on one axis, mounted inside the real page behind a fixed picker, every one clearing `anti-slop`, `better-ui` and `emil-design-eng` first. The verdict goes to the spec and `DESIGN.md`; the prototype goes to a `prototype/<name>` branch.

**4. Spec.** `/to-spec` synthesises the thread, no second interview: Problem, Outcome, User journeys, Requirements, Design, Implementation decisions, Testing decisions, Out of scope, Open questions. It confirms the test seams, publishes to the tracker (Linear, GitHub, or `.scratch/specs/`), and fills the PRD, roadmap and architecture rows itself.

**5. Tickets.** `/to-tickets` cuts the spec into vertical slices sized for one fresh session, each with its blocking edges, a **Read first** line, its seams and acceptance criteria. You approve the breakdown; it publishes in dependency order and moves the feature to Now on the roadmap.

**6. Build, one ticket per session.** `/implement <ticket>` claims it, reads `docs/agents/rules.md`, confirms the seams, drives `tdd` red-green at those seams, closes every slice through `verify`, runs `finish-screen` on any screen it produced, then `code-review` (Standards and Spec in parallel sub-agents), fixes every finding, updates the ticket and the roadmap count, commits. `experimental/implement-spec` does the whole graph instead with concurrent subagents in worktrees.

**7. Finish and review UI.** `finish-screen` rebuilds a screen in the project's idiom, ships every state (`loading`, `empty`, `error`, 320px), runs `anti-slop`, `mobile-first`, `better-ui`, `emil-design-eng`, `fix-copy`, clears the floor `DESIGN.md` names, proves it through `verify`, and marks the screen finished. `/refine-ui` is the polish-only pass. `/review-ui` reviews the branch or PR against the same catalogs and returns `Block` or `Approve`.

**8. Ask.** `/ask-farol` is the router when you forget which skill fits.

## Skills

Status: `stable` ships in the plugin; `experimental` lives in `experimental/` and is linked locally only. Invocation: `user` means you type it; `model` means the agent can reach it on its own and other skills can call it.

| Skill | Status | Invocation | Job |
| --- | --- | --- | --- |
| [ask-farol](./skills/ask-farol/SKILL.md) | stable | user | router over the set |
| [setup-farol-skills](./skills/setup-farol-skills/SKILL.md) | stable | user | tracker, agent docs, `DESIGN.md`, docs layout |
| [setup-verify](./skills/setup-verify/SKILL.md) | stable | user | detect the stack, prove commands and probes, write the project `verify` skill |
| [grill-me](./skills/grill-me/SKILL.md) | stable | user | relentless doc-aware interview, records terms and decisions |
| [grilling](./skills/grilling/SKILL.md) | stable | model | the interview primitive |
| [domain-modeling](./skills/domain-modeling/SKILL.md) | stable | model | glossary, ADRs, architecture boundaries |
| [codebase-explore](./skills/codebase-explore/SKILL.md) | stable | model | cited answers about this repo |
| [github-explore](./skills/github-explore/SKILL.md) | stable | model | clone, trace and translate an open-source repo |
| [prototype](./skills/prototype/SKILL.md) | stable | model | logic HTML file or UI variants behind a picker |
| [shape-ui](./skills/shape-ui/SKILL.md) | stable | user | design brief before code |
| [to-spec](./skills/to-spec/SKILL.md) | stable | user | conversation to spec, published |
| [to-tickets](./skills/to-tickets/SKILL.md) | stable | user | spec to session-sized tickets with edges |
| [implement](./skills/implement/SKILL.md) | stable | user | one ticket: tdd, verify, finish-screen, code-review, commit |
| [tdd](./skills/tdd/SKILL.md) | stable | model | red-green at pre-agreed seams |
| [code-review](./skills/code-review/SKILL.md) | stable | model | Standards and Spec axes in parallel |
| [finish-screen](./skills/finish-screen/SKILL.md) | stable | model | screen to production standard |
| [refine-ui](./skills/refine-ui/SKILL.md) | stable | user | polish-only pass |
| [fix-copy](./skills/fix-copy/SKILL.md) | stable | model | every string in the product voice |
| [mobile-first](./skills/mobile-first/SKILL.md) | stable | model | layout from 320px up |
| [review-ui](./skills/review-ui/SKILL.md) | stable | user | change-scoped UI review, Block or Approve |
| [rule](./skills/rule/SKILL.md) | stable | model | add a project convention: linter when possible, `docs/agents/rules.md` otherwise |
| [write-skill](./skills/write-skill/SKILL.md) | stable | user | write or review a skill |
| [writing-for-agents](./skills/writing-for-agents/SKILL.md) | stable | model | reference for documents agents consume (vendored) |
| [anti-slop](./skills/anti-slop/SKILL.md) | stable | model | AI-slop bans and the font, colour, structure procedures (impeccable) |
| [better-ui](./skills/better-ui/SKILL.md) | stable | model | exact polish values (vendored, Jakub Krehel) |
| [emil-design-eng](./skills/emil-design-eng/SKILL.md) | stable | model | animation decision framework (vendored, Emil Kowalski) |
| [implement-spec](./experimental/implement-spec/SKILL.md) | experimental | user | whole ticket graph with concurrent subagents, one PR |

Plugin version: see [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json). It bumps with every change under `skills/`.

## Docs a repo ends up with

| File | What it is for |
| --- | --- |
| `docs/agents/README.md` | index; read order |
| `docs/agents/navigation.md` | codebase map: stack, entry points, where things live, conventions, gotchas |
| `docs/agents/workflow.md` | the flow above and context hygiene |
| `docs/agents/issue-tracker.md` | where specs and tickets live, how to read and publish |
| `docs/agents/domain.md` | how to consume `CONTEXT.md` and ADRs |
| `docs/agents/rules.md` | project conventions, one row each, or a pointer to the tool that enforces them. Say "add a rule: ..." |
| `DESIGN.md` | design system: audience, tone, direction, tokens, components, motion, copy, bans, floor, decisions log |
| `.impeccable.md` | mirror of the Design Context so impeccable's own commands read the same truth |
| `docs/README.md` | registry: every doc, what, who writes it, when. Copy `docs/_template.md` and add a row to add one |
| `docs/product/{vision,prd,roadmap}.md` | why; capabilities with status; now / next / later |
| `docs/design/{brand,screens}.md` | identity beyond UI; every screen with states `L E R N` and status |
| `docs/architecture/overview.md` | contexts, containers, data, request paths, boundaries, debt |
| `CONTEXT.md`, `docs/adr/` | glossary and decisions, created lazily |
| `.claude/skills/verify/` | the project's own verify loop, generated by `/setup-verify` |
| `.scratch/` | specs and tickets (local tracker), explorations, prototypes, verify artifacts |

## Making new skills

New skills start in [`experimental/`](./experimental/), same shape as `skills/`: `SKILL.md`, `agents/openai.yaml`, sibling reference files. `/write-skill` walks the process (leading word, home, invocation, draft with completion criteria, prune, register). Promote to `skills/` once it has run for real: move the folder, add it to `plugin.json`, `ask-farol` and the table above, bump the version.
