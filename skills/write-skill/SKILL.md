---
name: write-skill
description: "Write or review a skill: pick invocation, draft SKILL.md, prune, place it in this project or in farol-skills, register it."
disable-model-invocation: true
---

# Write skill

Call the Skill tool with "writing-for-agents" first; it is the reference this process applies. Read its `SKILL-MECHANICS.md` when the document is a skill, which here it always is.

## Steps

1. **Name the job in one line** and the **leading word** the agent will think with (_loop_, _frontier_, _slop_). Without a leading word the skill is a checklist; keep looking until one fits. Done when both are written at the top of the draft.
2. **Pick the home**: this project (`.claude/skills/<name>/`, for a skill that only makes sense here, like `verify`) or farol-skills (`skills/<name>/`, for a skill any project would want). Done when the folder exists.
3. **Pick invocation**: model-invoked only when the agent must reach it alone or another skill must call it; otherwise user-invoked. Write the description accordingly: model-facing with one trigger per branch, or a human-facing one-liner. Done when the frontmatter is written and `agents/openai.yaml` matches it.
4. **Draft the body** as steps with a checkable completion criterion each, or as flat reference, or both. Inline what every branch needs; disclose what only some branches reach into a sibling file behind a pointer whose wording says when to open it. Done when every step ends on a criterion the agent can test.
5. **Prune** sentence by sentence: relevance, no-op, duplication, negation (rewrite as the positive target). Collapse restated triads into a leading word. Done when a second pass removes nothing.
6. **Register**: in farol-skills, add the skill to `.claude-plugin/plugin.json`, `README.md`, `ask-farol`, bump `plugin.json` version; in a project, add a line to `docs/agents/README.md` saying when to reach for it. Done when `claude plugin validate . --strict` passes (farol) or the pointer line exists (project).

## Review mode

Invoked with a path to an existing skill: run step 5 against it, then check steps 1, 3 and 4 and report each as a finding with the line and the fix. Apply the fixes when the user agrees.
