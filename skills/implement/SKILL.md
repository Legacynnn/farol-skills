---
name: implement
description: "Implement one ticket end to end in a fresh session: read the agent docs, build at the agreed seams test-first, finish any screen against DESIGN.md, review, commit."
disable-model-invocation: true
---

# Implement

One ticket per session. Fetch it per `docs/agents/issue-tracker.md` (claim it first where the tracker supports it), then read what its **Read first** line names.

1. Restate the ticket's **Delivers** line and acceptance criteria. Confirm the seams under test exist or agree the new one in one message.
2. Call the Skill tool with "tdd" and build at those seams, one red-green slice at a time. Typecheck and run the touched test files as you go; the full suite once at the end.
3. For any screen or component the ticket produces, call the Skill tool with "finish-screen".
4. Call the Skill tool with "code-review" against the branch point. Fix every finding.
5. Tick the acceptance criteria in the ticket, set its status to done, add a short log entry (what changed, anything the next ticket should know). Call the Skill tool with "sync-docs" for the event "ticket done". Commit to the current branch with the ticket id in the message.

Stop and report when a criterion cannot be met without a decision the ticket does not contain; never widen scope to make it fit.
