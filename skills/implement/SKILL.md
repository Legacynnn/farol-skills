---
name: implement
description: "Implement one ticket end to end in a fresh session: read the agent docs, build at the agreed seams test-first, finish any screen against DESIGN.md, review, commit."
disable-model-invocation: true
---

# Implement

One ticket per session. Fetch it per `docs/agents/issue-tracker.md` (claim it first where the tracker supports it), then read what its **Read first** line names and `docs/agents/rules.md`.

1. Restate the ticket's **Delivers** line and acceptance criteria. Confirm the seams under test exist or agree the new one in one message.
2. Call the Skill tool with "tdd" and build at those seams, one red-green slice at a time. Close every slice through the Skill tool with "verify" (static loop per slice, the surface's runtime loop and all tests before step 4); without a project `verify`, use `docs/agents/navigation.md` commands and tell the user to run `/setup-verify`.
3. For any screen or component the ticket produces, call the Skill tool with "finish-screen".
4. Call the Skill tool with "code-review" against the branch point. Fix every finding.
5. Tick the acceptance criteria in the ticket, set its status to done, add a short log entry (what changed, anything the next ticket should know). Bump the Now count in `docs/product/roadmap.md`; when this was the last ticket, move it to Shipped and set its `prd.md` rows to `shipped`. Commit to the current branch with the ticket id in the message.

Stop and report when a criterion cannot be met without a decision the ticket does not contain; never widen scope to make it fit.
