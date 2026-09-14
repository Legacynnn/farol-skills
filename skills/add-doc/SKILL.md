---
name: add-doc
description: "Add a new project doc under docs/ with the standard shape (frontmatter, fixed sections, update triggers, sources) and register it in docs/README.md."
disable-model-invocation: true
---

# Add doc

Grow the docs layout per project without losing the shape that keeps it agent-maintainable.

1. Take the doc's name and purpose from the arguments; ask for the purpose in one line if missing. Pick the folder: `product/`, `design/`, `architecture/`, or a new top-level folder the user names.
2. Draft it from the template in [`../setup-farol-skills/docs/_doc-template.md`](../setup-farol-skills/docs/_doc-template.md): frontmatter (`status`, `updated`, `owner`), a one-paragraph purpose, three to six fixed sections with `_none yet_` placeholders, **Update triggers** naming the events and the skill that fires them, **Sources**.
3. Propose the triggers explicitly: which events in the flow (spec, tickets, ticket done, screen, ADR, design rule, exploration) change this doc and what changes. A doc with no trigger will rot; say so if you cannot find one.
4. Show the draft; the user edits. Write it, then add its row to `docs/README.md` Registry: purpose, written by, changes when.
5. If a skill should now read this doc before acting, add the pointer to `docs/agents/README.md` read order.

Done when the file exists, the registry row exists, and every trigger names a real event.
