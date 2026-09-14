# farol-skills

Agent skills merged from three workflows (Matt Pocock's engineering flow, Jakub Krehel's `better-ui`, Emil Kowalski's `emil-design-eng`) into one set that reads a repo's agent docs before it acts. Documentation-only: no build, no tests.

## Layout

- `skills/<name>/SKILL.md` is the skill; supporting `.md` files sit beside it; `agents/openai.yaml` carries Codex metadata.
- `skills/setup-farol-skills/` holds the templates for the per-repo agent docs (`docs/agents/*.md`, `DESIGN.md`).
- `skills/better-ui/` and `skills/emil-design-eng/` are vendored verbatim from upstream (see `NOTICE.md`). Do not edit them here; re-sync from upstream instead.
- `.claude-plugin/plugin.json` lists every shipped skill; `.claude-plugin/marketplace.json` makes the repo its own marketplace. Bump `version` in `plugin.json` in the same commit as any change under `skills/`. Run `claude plugin validate . --strict` after touching either.
- `scripts/link-skills.sh` symlinks every skill into `~/.claude/skills` and `~/.agents/skills` for local use.

## Invariants

- Every skill is either **user-invoked** (`disable-model-invocation: true` plus `policy.allow_implicit_invocation: false` in `agents/openai.yaml`, human-facing description) or **model-invoked** (neither, description carries triggers). A user-invoked skill may call model-invoked ones through the Skill tool and never another user-invoked one.
- Dependencies are written as `Call the Skill tool with "<name>"`, one skill per call.
- Every skill that touches UI reads `DESIGN.md` first and loads `better-ui` and `emil-design-eng` for values. Rules live in those catalogs; farol skills own process, not values.
- Every skill that asks the user anything reads `docs/agents/README.md` and what it indexes first, and never asks what those files answer.
- `ask-farol` is the router. When a skill is added, renamed, removed, or changes where it sits in the flow, update `ask-farol`, `README.md`, `plugin.json`, and `setup-farol-skills/workflow.md`.
- No em-dashes in prose. No comments in scripts.
