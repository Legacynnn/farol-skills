# farol-skills

One skill set for the whole loop: explore, grill, prototype, spec, tickets, build, finish the screen. Every skill reads the repo's **agent docs** first (`docs/agents/`, `DESIGN.md`, `CONTEXT.md`) so nothing documented gets asked twice and no UI gets built off-system.

Merged and adapted from [mattpocock/skills](https://github.com/mattpocock/skills), [jakubkrehel/skills](https://github.com/jakubkrehel/skills) and [emilkowalski/skills](https://github.com/emilkowalski/skills). See `NOTICE.md`.

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

It configures the issue tracker (Linear, GitHub, or local `.scratch/`), writes the agent navigation docs under `docs/agents/`, and seeds `DESIGN.md`.

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
                   /implement <ticket>          fresh context per ticket, test-first, /finish-screen on screens
                   /review-ui                   before merge
```

`/ask-farol` is the router when you forget which one.

## Agent docs a repo ends up with

| File | What it is for |
| --- | --- |
| `docs/agents/README.md` | index; read order |
| `docs/agents/navigation.md` | codebase map: stack, entry points, where things live, conventions, gotchas |
| `docs/agents/workflow.md` | the flow above and context hygiene |
| `docs/agents/issue-tracker.md` | where specs and tickets live, how to read and publish |
| `docs/agents/domain.md` | how to consume `CONTEXT.md` and ADRs |
| `DESIGN.md` | the design system: audience, tone, tokens, components, motion, copy voice, decisions log. **Required by every UI skill** |
| `CONTEXT.md`, `docs/adr/` | glossary and decisions, created lazily by `domain-modeling` |
| `.scratch/` | specs, tickets (local tracker), explorations, prototypes |

## Reference

**User-invoked** (you type them; the agent never fires them on its own)

- [ask-farol](./skills/ask-farol/SKILL.md): router over the set.
- [setup-farol-skills](./skills/setup-farol-skills/SKILL.md): once per repo; tracker, agent docs, `DESIGN.md`.
- [grill-me](./skills/grill-me/SKILL.md): relentless interview that reads the docs first and records terms and decisions.
- [to-spec](./skills/to-spec/SKILL.md): conversation to spec (problem, journeys, requirements, decisions), published to the tracker.
- [to-tickets](./skills/to-tickets/SKILL.md): spec to session-sized vertical slices with blocking edges.
- [implement](./skills/implement/SKILL.md): one ticket, fresh session, test-first, finished screens, reviewed, committed.
- [shape-ui](./skills/shape-ui/SKILL.md): plan a screen before code; brief plus `DESIGN.md` updates.
- [refine-ui](./skills/refine-ui/SKILL.md): polish pass against the craft catalogs.
- [fix-copy](./skills/fix-copy/SKILL.md): every string in the product voice.
- [mobile-first](./skills/mobile-first/SKILL.md): rebuild a layout from 320px up.
- [finish-screen](./skills/finish-screen/SKILL.md): prototype winner or rough screen to production standard.
- [review-ui](./skills/review-ui/SKILL.md): change-scoped UI review with a Block/Approve verdict.

**Model-invoked** (you or the agent)

- [grilling](./skills/grilling/SKILL.md): the interview primitive, doc-aware.
- [domain-modeling](./skills/domain-modeling/SKILL.md): glossary and ADR discipline.
- [codebase-explore](./skills/codebase-explore/SKILL.md): answer a question about this repo with citations; notes to `.scratch/explorations/`.
- [github-explore](./skills/github-explore/SKILL.md): clone a GitHub URL into a cache, explain how something works inside it, note what transfers.
- [prototype](./skills/prototype/SKILL.md): logic prototype as one HTML file, or UI variants behind a fixed picker styled from `DESIGN.md`.
- [better-ui](./skills/better-ui/SKILL.md): exact values for radii, shadows, icons, enter/exit, performance. Vendored from Jakub Krehel.
- [emil-design-eng](./skills/emil-design-eng/SKILL.md): animation decision framework, springs, gestures, review table. Vendored from Emil Kowalski.
