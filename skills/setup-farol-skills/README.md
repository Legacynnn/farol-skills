# Agent docs

Read in this order before exploring the codebase or asking the user a question. Anything answered here is never asked again.

1. [navigation.md](./navigation.md): where things are, how to run and test, conventions.
2. [workflow.md](./workflow.md): the flow from idea to shipped ticket, and where you are in it.
3. [issue-tracker.md](./issue-tracker.md): where specs and tickets live, how to read and publish them.
4. [domain.md](./domain.md): how to use `CONTEXT.md` and ADRs.
5. [rules.md](./rules.md): project conventions. Read before writing code; `code-review` checks against it.
6. `../../DESIGN.md`: the design system. Mandatory before any UI work.
7. `../../CONTEXT.md`: the domain glossary, if present.
8. `../../.claude/skills/verify/SKILL.md`: how to prove a change works here; every loop closes on it. Missing means `/setup-verify` has not run.
9. [../README.md](../README.md): the registry of product, design and architecture docs. Open the ones the task names; `architecture/overview.md` before any structural change, `product/vision.md` before any spec.

If a file is missing, proceed silently. Skills create `CONTEXT.md` and `docs/adr/` lazily.
