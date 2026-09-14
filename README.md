# farol-skills

One skill set for the whole loop: explore, grill, prototype, spec, tickets, build, finish the screen. Every skill reads the repo's **agent docs** first (`docs/agents/`, `DESIGN.md`, `CONTEXT.md`) so nothing documented gets asked twice and no UI gets built off-system.

Merged and adapted from [mattpocock/skills](https://github.com/mattpocock/skills), [jakubkrehel/skills](https://github.com/jakubkrehel/skills), [emilkowalski/skills](https://github.com/emilkowalski/skills) and [impeccable](https://impeccable.style). See `NOTICE.md`.

## Install

Claude Code plugin (read-only, updates with the repo):

```
/plugin marketplace add legacyn/farol-skills
/plugin install farol-skills@farol
```

Local symlinks for any harness (Claude Code and Codex), from a clone:

```bash
scripts/link-skills.sh
```

Then, once per repo:

```
/setup-farol-skills
```

It configures the issue tracker (Linear, GitHub, or local `.scratch/`), writes the agent navigation docs under `docs/agents/`, seeds `DESIGN.md`, and scaffolds the project docs layout below.

## The flow

```
/codebase-explore  /github-explore <url>        explore, notes land in .scratch/explorations/
        └──────────────┬─────────────┘
                   /grill-me                    interview, reads docs first, writes CONTEXT.md + ADRs
                  ┌────┴────┐
              /shape-ui  /prototype             UX brief per screen; logic HTML or UI variants behind a picker
                  └────┬────┘
                   /to-spec                     problem, journeys, requirements, decisions
                   /to-tickets                  session-sized vertical slices with blocking edges
                   /implement <ticket>          fresh context per ticket: tdd, UI catalogs, code-review
                   /implement-spec              experimental: whole ticket graph, concurrent subagents, one PR
                   /review-ui                   before merge (finish-screen runs inside implement)
```

`/ask-farol` is the router when you forget which one.

## Docs a repo ends up with

| File | What it is for |
| --- | --- |
| `docs/agents/README.md` | index; read order |
| `docs/agents/navigation.md` | codebase map: stack, entry points, where things live, conventions, gotchas |
| `docs/agents/workflow.md` | the flow above and context hygiene |
| `docs/agents/issue-tracker.md` | where specs and tickets live, how to read and publish |
| `docs/agents/domain.md` | how to consume `CONTEXT.md` and ADRs |
| `DESIGN.md` | the design system: audience, tone, direction, tokens, components, motion, copy voice, bans, decisions log. **Required by every UI skill** |
| `.impeccable.md` | mirror of the Design Context so impeccable's own commands read the same truth |
| `CONTEXT.md`, `docs/adr/` | glossary and decisions, created lazily by `domain-modeling` |
| `.scratch/` | specs, tickets (local tracker), explorations, prototypes |
| `docs/README.md` | the registry: every doc, its purpose, who writes it, when it changes. Add a row to add a doc |
| `docs/product/vision.md` | one line, users, problems, principles, bets, not-this, measures |
| `docs/product/prd.md` | capabilities per journey with status and spec pointer |
| `docs/product/roadmap.md` | now / next / later / shipped / dropped |
| `docs/design/brand.md` | name, story, voice, marks, imagery, feel |
| `docs/design/screens.md` | every screen: route, purpose, primary action, states `L E R N`, status, spec |
| `docs/architecture/overview.md` | context, contexts, containers, data, request paths, cross-cutting, boundaries, debt |

Every doc carries frontmatter (`status`, `updated`, `owner`), fixed sections that stay even when empty, an **Update triggers** block, and **Sources**. `sync-docs` fires events (spec published, ticket done, screen finished, ADR written) against the triggers; `/add-doc` adds a doc in the same shape and registers it.

## Reference

**User-invoked** (you type them; the agent never fires them on its own)

- [ask-farol](./skills/ask-farol/SKILL.md): router over the set.
- [setup-farol-skills](./skills/setup-farol-skills/SKILL.md): once per repo; tracker, agent docs, `DESIGN.md`.
- [grill-me](./skills/grill-me/SKILL.md): relentless interview that reads the docs first and records terms and decisions.
- [to-spec](./skills/to-spec/SKILL.md): conversation to spec (problem, journeys, requirements, decisions), published to the tracker.
- [to-tickets](./skills/to-tickets/SKILL.md): spec to session-sized vertical slices with blocking edges.
- [implement](./skills/implement/SKILL.md): one ticket, fresh session, `tdd` at the seams, UI catalogs on screens, `code-review`, committed.
- [implement-spec](./skills/implement-spec/SKILL.md): **experimental**. The whole ticket graph with concurrent implementer subagents in worktrees, merger subagents, one reviewed PR.
- [shape-ui](./skills/shape-ui/SKILL.md): plan a screen before code; brief plus `DESIGN.md` updates.
- [refine-ui](./skills/refine-ui/SKILL.md): polish pass against the craft catalogs.
- [review-ui](./skills/review-ui/SKILL.md): change-scoped UI review with a Block/Approve verdict.
- [add-doc](./skills/add-doc/SKILL.md): add a project doc in the standard shape and register it.

**Model-invoked** (you or the agent)

- [grilling](./skills/grilling/SKILL.md): the interview primitive, doc-aware.
- [domain-modeling](./skills/domain-modeling/SKILL.md): glossary and ADR discipline.
- [codebase-explore](./skills/codebase-explore/SKILL.md): answer a question about this repo with citations; notes to `.scratch/explorations/`.
- [github-explore](./skills/github-explore/SKILL.md): clone a GitHub URL into a cache, explain how something works inside it, note what transfers.
- [prototype](./skills/prototype/SKILL.md): logic prototype as one HTML file, or UI variants behind a fixed picker styled from `DESIGN.md`.
- [tdd](./skills/tdd/SKILL.md): red-green loop at pre-agreed seams.
- [code-review](./skills/code-review/SKILL.md): two-axis diff review, Standards and Spec, parallel sub-agents.
- [fix-copy](./skills/fix-copy/SKILL.md): every string in the product voice.
- [mobile-first](./skills/mobile-first/SKILL.md): rebuild a layout from 320px up.
- [finish-screen](./skills/finish-screen/SKILL.md): prototype winner or rough screen to production standard; `implement` calls it on every screen.
- [sync-docs](./skills/sync-docs/SKILL.md): walk every doc's update triggers for an event and edit only what they name.
- [anti-slop](./skills/anti-slop/SKILL.md): the AI-slop bans and the font, colour, structure procedures that replace reflex defaults. Distilled from impeccable.style, references vendored.
- [better-ui](./skills/better-ui/SKILL.md): exact values for radii, shadows, icons, enter/exit, performance. Vendored from Jakub Krehel.
- [emil-design-eng](./skills/emil-design-eng/SKILL.md): animation decision framework, springs, gestures, review table. Vendored from Emil Kowalski.
