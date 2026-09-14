---
name: implement-spec
description: "Experimental. Implement a whole spec on one branch by working its ticket graph with concurrent implementer subagents in worktrees, merging as the frontier moves, ending in one reviewed PR."
disable-model-invocation: true
---

# Implement spec

One spec, one branch, one PR. The tickets are a **task graph**, not a list: there is always a **frontier** of tickets whose blockers are done, and every ticket on it can run at once.

You are the coordinator. You never implement; you dispatch, merge, and keep the frontier moving. Communication with subagents is **context pointers** (spec, ticket, exploration notes, commits), never restated content.

Everything a subagent must read is in the repo: `docs/agents/README.md` and what it indexes, the spec, its ticket, `DESIGN.md` when the ticket has a screen.

## Steps

1. **Load the graph.** Fetch the spec and every ticket per `docs/agents/issue-tracker.md`. Build the table: ticket, blockers, status. Done when every ticket has a row and no blocker points at a missing ticket.
2. **Explore once.** If tickets need codebase or external knowledge that is not yet in `.scratch/explorations/`, dispatch one exploration subagent running `codebase-explore` or `github-explore` and let it write the notes there. Done when every ticket's "Read first" line resolves to existing files.
3. **Open the branch.** `feature/<spec-slug>` off the default branch; a draft PR that closes the spec and every ticket (GitHub) or links them (Linear, local). Record the branch name and PR URL in the spec's log.
4. **Dispatch the frontier.** For each unblocked, unclaimed ticket, claim it in the tracker and start an **implementer subagent** in the background, in its own worktree on `feature/<spec-slug>/<ticket>`, with this brief and nothing more:

   > Implement ticket <id> at <path or url>. Read `docs/agents/README.md` first. Call the Skill tool with "tdd" at the seams the ticket names and close every slice with "verify". For any screen, call the Skill tool with "finish-screen". Commit on your branch with the ticket id in the message. Report: commits, criteria met, criteria not met and why, anything the next ticket must know. Under 200 words.

5. **Merge as they land.** When an implementer reports, a **merger subagent** rebases its branch onto `feature/<spec-slug>`, resolves conflicts by intent (each side's ticket is the primary source), runs typecheck and the touched tests, merges, and marks the ticket done with a one-line log. A red merge goes back to a fresh implementer with the failure output, never to the merger to fix.
6. **Recompute the frontier** after every merge and return to step 4. Done when every ticket is done.
7. **Review.** Call the Skill tool with "code-review" against the default branch. Fix every finding in a single implementer subagent on the PR branch. Tell the user which screens changed so they can run `/review-ui`.
8. **Ready.** Full test suite green, PR marked ready, spec log updated with what shipped and what was left open. Remove every worktree.

## Rules

- Concurrency is bounded by conflict risk: two tickets touching the same files run in sequence even when both are unblocked. Say when you serialised and why.
- A ticket an implementer cannot finish without a decision stops that ticket, not the run. Record the question in the ticket, keep the rest moving, and put every open question in front of the user at the end.
- Nothing merges red.
