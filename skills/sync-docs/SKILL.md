---
name: sync-docs
description: Bring the project docs up to date with what just happened, by walking each doc's Update triggers in the docs registry. Use after a spec, tickets, ticket completion, screen, ADR or design rule lands, or when the user asks to update, sync or refresh the docs.
---

# Sync docs

The docs in `docs/` stay true because every one of them declares its **Update triggers**. This skill fires an event against those triggers and edits only what they name.

1. **Name the event** in one line: what landed (spec published, tickets published, ticket done, screen finished, ADR written, design rule settled, module or integration changed) and its pointer (path, id, commit).
2. **Read the registry**, `docs/README.md`. For each doc in the table, read its **Update triggers** section. Collect every trigger the event matches. A doc without a matching trigger is not opened.
3. **Edit each matched doc**: replace the line the trigger names, keep the fixed sections, set `updated` in the frontmatter, add the pointer under **Sources** when it is new. Growth is by replacement; a doc that only gets longer is being appended to, not synced.
4. **Cross-check the registry itself**: a doc referenced by the event that has no row (a new spec folder, a new screen with no `screens.md` row) gets one, in the shape the template shows.
5. **Report** as a table `| Doc | Trigger | Change |`, and list docs whose triggers matched but whose content you could not fill from the event, so the user fills them.

Done when every matched trigger has a row in the report.
