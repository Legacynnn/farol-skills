---
name: review-ui
description: Review the UI in a change (uncommitted work, branch, or PR) against DESIGN.md and the craft catalogs, reporting ranked findings with a Block or Approve verdict.
disable-model-invocation: true
---

# Review UI

A change review, not a screen review: what did this diff make worse? Read-only.

1. Resolve scope, first match wins: the target the user named (`pr 42`, a branch, a range), else commits ahead of the merge base plus uncommitted changes, else the dirty tree, else stop and ask; never fall back to `HEAD~1` alone. Exclude lockfiles, snapshots, generated output; say what was excluded.
2. Expand changed files one hop to the surfaces they render in; two hops for tokens and shared primitives. Review at most five consumers and say how many were not expanded.
3. Read `DESIGN.md`. A documented convention decides where a finding is reported, never whether it is one.
4. Call the Skill tool three times, for "anti-slop", "better-ui" and "emil-design-eng", and apply all three catalogs to the changed surfaces. Check the floor `DESIGN.md` names under Patterns, and the copy against its voice.
5. Classify each finding `Introduced`, `Regression`, or `Pre-existing`. Only the first two count toward the verdict; list at most three pre-existing ones in their own section.
6. Report:

**Scope**: what was reviewed and what was excluded.

| Severity | Status | Location | Before | After | Why |
| --- | --- | --- | --- | --- | --- |

`HIGH` blocks a task, hides content, or breaks the accessibility floor. `MEDIUM` harms comprehension or consistency. `LOW` is isolated polish. One root cause is one row with every location.

**Verification**: the `verify` loops run (call the Skill tool with "verify" when the project has one), states walked, and everything `Not verified`.

**Verdict**: `Block` when any `HIGH` remains, else `Approve`. Never approve coverage not inspected.
