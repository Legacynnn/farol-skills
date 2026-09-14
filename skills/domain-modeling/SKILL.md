---
name: domain-modeling
description: Build and sharpen a project's domain model. Use when discussing codebase terminology, writing or editing a CONTEXT.md, or recording or editing an ADR.
---

# Domain Modeling

Actively build and sharpen the project's domain model as you design: challenge terms, invent edge-case scenarios, write the glossary and decisions down the moment they crystallise. Reading `CONTEXT.md` for vocabulary is not this skill; changing the model is.

Layout is described in `docs/agents/domain.md`. Create files lazily: `CONTEXT.md` when the first term resolves, `docs/adr/` when the first ADR is needed.

## During the session

- **Challenge against the glossary.** A term that conflicts with `CONTEXT.md` gets called out immediately: "Your glossary defines 'cancellation' as X, but you seem to mean Y. Which is it?"
- **Sharpen fuzzy language.** Overloaded words get a proposed canonical term: "'account': Customer or User? Those are different."
- **Discuss concrete scenarios.** Stress-test relationships with specific edge cases that force precise boundaries.
- **Cross-reference with code.** When the user states how something works, check the code agrees, and surface contradictions.
- **Update `CONTEXT.md` inline**, the moment a term resolves, using [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md). The glossary holds no implementation detail; it is a glossary and nothing else.
- **Offer ADRs sparingly**, only when all three hold: hard to reverse, surprising without context, the result of a real trade-off. Format in [ADR-FORMAT.md](./ADR-FORMAT.md).
- **Design decisions go to `DESIGN.md`**, not to an ADR: a settled visual or interaction rule is one line in its Decisions log.
- **After an ADR lands**, call the Skill tool with "sync-docs" for the event "ADR written", so `docs/architecture/overview.md` carries the rule.
