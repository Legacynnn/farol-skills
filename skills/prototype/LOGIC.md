# Logic prototype

One self-contained HTML file (a **shareable demo**) that lets anyone drive a state model by clicking buttons. For business logic, state transitions, data shape: the kind of thing that looks fine on paper and only feels wrong under real cases.

Hand it to a designer, PM, or domain expert. It speaks their language (`CONTEXT.md` terms), not the code's.

## Process

1. **State the question** in one visible paragraph at the top of the page.
2. **Isolate the logic in a portable module**: one `<script>` block holding a pure reducer `(state, action) => state`, a state machine, a set of pure functions, or a class with a clear surface. No DOM inside it. The page calls it; nothing flows back. This module is the part that lifts into the real code later.
3. **Build the page**, plain HTML/CSS/JS, no framework, no server. Top to bottom: title and question; current state as a labelled panel re-rendered after every click, with what changed called out; free-play buttons, one per action; guided walkthroughs as tabs, each a plain-language scenario with ordered real buttons, resetting to a known state on start. Pick scenarios that probe the awkward cases: happy path, an edge case, an attempt at something that should be illegal.
4. **Style from `DESIGN.md`**: its type, one accent, its spacing. Restrained, no animation. Save under `.scratch/prototypes/<name>/index.html`.
5. **Hand it over.** The interesting moments are "wait, that shouldn't be possible". Add actions and scenarios as they ask; prototypes evolve.
6. **Capture.** The validated module lifts into the real code; the spec inlines the decision-rich part (the state table, the reducer signature) with a note that it came from a prototype. The HTML rides to the `prototype/<name>` branch.

## Anti-patterns

No tests. No real database. No generalising for later. No DOM in the logic module. No framework or bundler. No shipping the shell.
