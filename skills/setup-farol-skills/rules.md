# Rules

Project conventions the code does not enforce by itself. Every rule is one row, phrased as the thing to do, with the reason and the alternative. `code-review` checks the diff against this table; `implement` and `tdd` read it before writing. A rule a tool can enforce lives in the tool's config and is listed here only by pointer.

Add a rule with the `rule` skill ("add a rule: ..."), or add a row by hand.

| Rule | Why | Instead of | Scope | Enforced by |
| --- | --- | --- | --- | --- |
| Derive state during render; reach for `useEffect` only to sync with something outside React (network, DOM, subscriptions) | effects that set state cause extra renders and hide data flow | `useEffect` + `setState` to compute a value | `**/*.tsx` | review |
| <rule> | <why> | <the reflex it replaces> | <glob> | `review` or `<tool: rule id>` |

## Enforced by tools

Pointers only; the config is the source of truth.

- `<eslint>`: `<path>`; rules that exist because of a row above: `<rule ids>`
- `<tsconfig strict>`: `<path>`
