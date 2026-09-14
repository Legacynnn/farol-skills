---
name: verify
description: Prove a change works in this project with evidence. Use after any code change, before reporting done, when a test or screen must be checked, or when another skill needs a red/green loop here.
---

# Verify

A **loop** closes on **evidence**: exit code, screenshot, snapshot, log. Never on "should work". Run the smallest loop that covers the change, then the next larger one before reporting done.

## Static loops

| Loop | Command | Green |
| --- | --- | --- |
| Typecheck | `<cmd>` | exit 0 |
| Lint | `<cmd>` | exit 0 |
| One test file | `<cmd> <path>` | exit 0, `n passed` |
| All tests | `<cmd>` | exit 0 |
| Build | `<cmd>` | exit 0 |

## Runtime loops

One per surface. Launch, observe, stop.

### <Surface, e.g. Web app>

- **Launch**: `<cmd>` → `<url>`; ready when `<log line or curl>` returns.
- **Observe**: `<tool, e.g. Chrome MCP: navigate url, screenshot, read console>`; artifact at `<path>`.
- **Prove a screen**: navigate to the route, check the states (`loading`, `empty`, `error`, 320px), read the console for errors.
- **Stop**: `<cmd>`.

## The loop

1. Name the claim: "after this change, X is true" with what evidence proves it.
2. Run the smallest loop that can go red on the claim. If it is green before the change, the loop is wrong; pick another.
3. Make the change. Run the loop. Read the evidence, not the exit code alone.
4. Widen: the surface's runtime loop, then all tests.
5. Report evidence by path or excerpt. A loop that could not be run is `Not verified`, named as such.

## Known gaps

- `<tool not installed, and what to install>`
