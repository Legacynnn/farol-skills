---
name: setup-verify
description: "Generate this project's verify skill: detect the stack, work out how an agent can run, observe and prove a change works here, and write .claude/skills/verify so every flow skill closes a loop on evidence."
disable-model-invocation: true
---

# Setup verify

Every project gets its own **verify** skill: the loop an agent runs to prove a change works, using this project's real tools. Farol skills call it; they never guess at commands.

The leading word is **evidence**: an exit code, a screenshot, a DOM snapshot, a log line, a simulator frame. A loop closes on evidence, never on "it should work".

## Steps

1. **Detect the stack.** Read `docs/agents/navigation.md`, the package manifest, lockfile, config files, `Makefile`/`justfile`, CI config, the routes and entry points. Classify every surface the project has (one project can have several): web app, API, CLI, library, Electron, Tauri, Expo/React Native, iOS, Android, browser extension. Done when each surface is named with the file that proves it.
2. **Prove each command.** For every check the project offers (typecheck, lint, one test file, all tests, build, e2e), find the real command and run it once. Record the exact invocation and what green looks like. A command that fails on a clean tree is a finding for the user, not a command to record. Done when every recorded command has been run.
3. **Choose the runtime probe per surface** from [stacks.md](stacks.md). Prove it works here: launch, observe (screenshot, snapshot, log, curl), stop. Record the exact steps, the URL or device, and the artifact path. Done when one observation per surface has been captured.
4. **Write the skill** to `.claude/skills/verify/SKILL.md` from [template.md](template.md), model-invoked, filled with only what steps 2 and 3 proved. Where an MCP or tool was missing (no simulator, no Chrome MCP), write the fallback that was proven and a one-line note of what to install. Done when the file contains no placeholder.
5. **Register**: a line in `docs/agents/README.md` read order (`.claude/skills/verify/SKILL.md`: how to prove a change works; every loop closes on it) and the commands mirrored into `docs/agents/navigation.md` Run it. Done when both pointers exist.
6. **Run it once** through the Skill tool on a trivial change (a whitespace edit, reverted after) and show the user the evidence it produced.

Re-run this skill when the stack changes; `verify` is regenerated, never hand-patched around a stale command.
