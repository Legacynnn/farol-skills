# farol-skills

Agent skills merged from four sources (Matt Pocock's engineering flow, Jakub Krehel's `better-ui`, Emil Kowalski's `emil-design-eng`, impeccable.style's anti-slop rules) into one set that reads a repo's agent docs before it acts. Documentation-only: no build, no tests.

## Layout

- `skills/<name>/SKILL.md` is the skill; supporting `.md` files sit beside it; `agents/openai.yaml` carries Codex metadata.
- `skills/setup-farol-skills/` holds the templates for the per-repo docs: `docs/agents/*.md`, `DESIGN.md`, and the project docs layout under `docs/` (registry, product, design, architecture). Every project doc template carries frontmatter (`owner` names the writing skill), fixed sections and **Sources**. The skill that produces a change writes the doc; there is no sync skill.
- `skills/better-ui/`, `skills/emil-design-eng/`, `skills/tdd/`, `skills/code-review/`, `skills/writing-for-agents/` and `skills/anti-slop/reference/` are vendored from upstream (see `NOTICE.md`); `tdd` and `code-review` carry only the setup pointer and doc-path edits. Re-sync from upstream rather than editing here.
- `.claude-plugin/plugin.json` lists every shipped skill; `.claude-plugin/marketplace.json` makes the repo its own marketplace. Bump `version` in `plugin.json` in the same commit as any change under `skills/`. Run `claude plugin validate . --strict` after touching either.
- `scripts/link-skills.sh` symlinks every skill into `~/.claude/skills` and `~/.agents/skills` for local use.

- `experimental/<name>/` is where a new skill incubates: same shape as `skills/`, linked locally by `scripts/link-skills.sh`, absent from `plugin.json` and from `ask-farol`. Promote by moving the folder to `skills/`, adding it to `plugin.json`, `README.md` and `ask-farol`, and bumping the version. A skill starts in `experimental/` unless it replaces an existing one.

## Invariants

- Every skill is either **user-invoked** (`disable-model-invocation: true` plus `policy.allow_implicit_invocation: false` in `agents/openai.yaml`, human-facing description) or **model-invoked** (neither, description carries triggers). A user-invoked skill may call model-invoked ones through the Skill tool and never another user-invoked one.
- Dependencies are written as `Call the Skill tool with "<name>"`, one skill per call.
- Every skill that touches UI reads `DESIGN.md` first and loads `anti-slop`, `better-ui` and `emil-design-eng` for values. Rules live in those catalogs; farol skills own process, not values.
- Every skill that asks the user anything reads `docs/agents/README.md` and what it indexes first, and never asks what those files answer.
- `ask-farol` is the router. When a skill is added, renamed, removed, or changes where it sits in the flow, update `ask-farol`, `README.md`, `plugin.json`, and `setup-farol-skills/workflow.md`.
- `setup-verify` writes a **project** skill at `.claude/skills/verify/`; farol skills reach it as `Call the Skill tool with "verify"` and fall back to `docs/agents/navigation.md` commands when it is absent.
- No em-dashes in prose. No comments in scripts.
