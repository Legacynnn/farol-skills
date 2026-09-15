---
name: rule
description: Add or change a project rule. Use when the user says add a rule, we should always or never, stop doing X, prefer Y, or states a code convention, and when code-review finds a repeated finding worth making a rule.
---

# Rule

A **rule** is a convention the project wants every session to obey. It lives in one of two places: the tool that can enforce it, or one row in `docs/agents/rules.md`. A rule in prose that a linter could hold is a cache of a lookup; put it in the tool.

1. **Phrase the target.** Rewrite what the user said as the thing to do, with the reason and the reflex it replaces. "Avoid too many useEffects" becomes "Derive state during render; reach for `useEffect` only to sync with something outside React", why: effects that set state hide data flow, instead of: effect + setState to compute a value. Done when the row has all three cells and no prohibition stands alone.
2. **Find the enforcer.** Check the project's linter, type config, formatter and test setup (`docs/agents/navigation.md` names them) for an existing rule that holds it, or one that can be enabled or written in a few lines (an ESLint `no-restricted-syntax` selector, a `tsconfig` flag, a custom rule, a test). Done when you can name the tool and rule id, or state that none applies.
3. **Install it.** Tool: change the config, run the linter once, record the pointer under *Enforced by tools* in `rules.md`. Judgment: add the row to the table with its scope glob and `review` in the last column. Done when the file is written and, for a tool, the run is green or its failures are listed.
4. **Measure the debt.** Grep or lint for current violations; report the count and the top three locations. Offer a ticket when the count is more than a session's work; never fix them inside this skill.

Done when `rules.md` has the row or pointer, the enforcer ran or was declared absent, and the violation count is reported.
