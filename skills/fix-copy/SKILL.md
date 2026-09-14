---
name: fix-copy
description: Rewrite UI copy (labels, buttons, errors, empty states, helper text) in the DESIGN.md voice and CONTEXT.md vocabulary. Use when the user mentions copy, microcopy, wording, labels, error messages, or when finish-screen or implement produce a screen.
---

# Fix copy

Words are interface. This pass rewrites every user-facing string on the target so it is clear, consistent, and in the product's voice.

1. Resolve the target: named path or route, else the uncommitted UI changes.
2. Read `DESIGN.md` (Copy section) and `CONTEXT.md`. Voice comes from the first, nouns from the second. A term listed under `_Avoid_` never appears on screen.
3. Collect every string on the target: labels, buttons, headings, placeholders, helper text, tooltips, errors, toasts, empty states, confirmations, `aria-label`s.
4. Rewrite against these rules:
   - Buttons are verbs naming the outcome (`Save changes`, `Delete project`), never `Submit`, `OK`, `Yes`.
   - Errors say what happened and how to recover, in that order, no blame, no jargon, no error codes as the message.
   - Empty states say what belongs here and offer the primary action.
   - Destructive confirmations name the thing (`Delete "Q3 report"?`) and the consequence.
   - Sentence case unless `DESIGN.md` says otherwise. No exclamation marks. No "please". No "successfully".
   - One term per concept across the whole target. Shorter wins when meaning holds.
   - Placeholders are examples, never labels.
5. Apply in place. Report a table `| Location | Before | After | Why |`. Add any new voice rule to `DESIGN.md`'s Copy section.
