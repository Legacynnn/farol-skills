---
name: prototype
description: Build a throwaway prototype to answer a design question. Use when the user wants to sanity-check whether a state model or logic feels right, or explore what a UI should look like before committing to a spec.
---

# Prototype

A prototype is **throwaway code that answers a question**. The question decides the shape:

- **"Does this logic / state model feel right?"** → [LOGIC.md](LOGIC.md). One shareable HTML file a non-developer can drive.
- **"What should this look like?"** → [UI.md](UI.md). Three to five variants that disagree on structure, behind a fixed picker, styled from `DESIGN.md`.

Ambiguous and the user unreachable: pick from the surrounding code (backend module → logic; page or component → UI) and state the assumption at the top of the prototype.

## Rules for both

1. **Read the docs first.** `docs/agents/navigation.md` for the prototype route convention and run command, `DESIGN.md` for tokens and voice, `CONTEXT.md` for labels. A prototype in the wrong vocabulary or off-system tokens answers the wrong question.
2. **Throwaway from day one, marked as such.** Close to where it will live, named so a reader sees `prototype` in the path.
3. **Trivial to run.** One command from the project's task runner, or one double-click.
4. **No persistence.** In-memory state unless persistence is the question; then a scratch store named `PROTOTYPE`.
5. **Skip the polish.** No tests, no error handling beyond runnable, no abstractions.
6. **Surface the state.** Every action (logic) or variant switch (UI) shows the full relevant state.
7. **Capture when done.** Fold the validated decision into the spec or `DESIGN.md`; commit the prototype to a `prototype/<name>` branch off main and point to it from the spec or ticket. Main keeps only the decision.
