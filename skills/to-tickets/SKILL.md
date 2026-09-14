---
name: to-tickets
description: Break a spec or the current conversation into tickets, each a vertical slice sized for one session, each declaring what blocks it, published to the configured tracker.
disable-model-invocation: true
---

# To tickets

Break the work into **tickets**: vertical slices, each small enough for one fresh context window, each declaring the tickets that **block** it. Tickets are the unit of coordination: any agent or human can pick up any unblocked ticket without the others' context.

`docs/agents/issue-tracker.md` says where tickets go. If missing, tell the user to run `/setup-farol-skills`.

## Process

### 1. Gather

Work from context. If the user passes a spec path, an issue id, or a URL, fetch it whole, including comments.

### 2. Explore, if needed

Read `docs/agents/navigation.md` and the code the spec touches. Ticket titles use `CONTEXT.md` terms. Look for prefactoring that makes the change easy; it goes first.

### 3. Draft vertical slices

<slice-rules>

- Each slice cuts a narrow but COMPLETE path through every layer it needs (schema, API, UI, tests). Vertical, never a layer.
- Done means demoable or verifiable on its own, with the states `DESIGN.md` requires when a screen is involved.
- Sized for one session: a fresh agent reads the ticket and the agent docs and finishes without asking.
- Prefactoring first. Wide mechanical refactors go expand → migrate in batches → contract, each batch its own ticket.

</slice-rules>

Give each ticket its **blocking edges**. A ticket with none can start now.

### 4. Quiz the user

Present a numbered list: **Title**, **Blocked by**, **Delivers** (the end-to-end behaviour). Ask: granularity right? edges correct? merge or split any? Iterate until approved.

### 5. Publish

Per the tracker doc, in dependency order so blockers have identifiers first. Local: one file per ticket under `.scratch/specs/<slug>/tickets/NN-<slug>.md`. Linear or GitHub: one issue per ticket, parent set to the spec, native blocking links. Never close or edit the parent spec.

<ticket-template>

# <NN>: <Ticket title>

**Delivers:** the end-to-end behaviour, from the user's perspective.

**Blocked by:** <numbers/ids> or "None (can start immediately)".

**Status:** ready

**Read first:** `docs/agents/README.md`, the spec at <path or url>, `DESIGN.md` sections <names> (when UI).

**Seams under test:** <the seams from the spec this ticket exercises>.

- [ ] Acceptance criterion 1
- [ ] Acceptance criterion 2
- [ ] States: loading, empty, error, 320px (when UI)

**Notes:** prototype branch, exploration notes, ADRs that constrain this ticket, by link.

</ticket-template>

No file paths or code in tickets except a prototype snippet that encodes a decision, trimmed and marked.

Then call the Skill tool with "sync-docs" for the event "tickets published".
