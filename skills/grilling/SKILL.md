---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea, after reading the agent docs so nothing already documented gets asked. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

## Read before asking

Before the first round, read the agent docs: `docs/agents/README.md` and everything it indexes, `DESIGN.md`, `CONTEXT.md`, ADRs in the area. A question those files answer is never asked; cite the file instead ("`DESIGN.md` says mobile first, so I assume the list collapses to one column, correct?"). When the docs disagree with what the user says, surface the conflict as a question. When a fact is in neither the docs nor the user's head but in the environment (filesystem, git, a dependency), dispatch a sub-agent for it; facts are your job, decisions are the user's.

## Rounds

The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard. Ask the whole frontier in one round, number each question, give your recommended answer. Then wait.

```
❓ **Q1** - **<question title>**: <question body, may include options>

➡️ <your recommended answer>

---

❓ **Q2** - **<question title>**: <question body>

➡️ <your recommended answer>
```

Each answered round reshapes the tree: settled decisions push the frontier outward. A question that depends on another still open in this round belongs to a later round. A running sub-agent is an unsettled prerequisite: only its downstream questions wait.

For a UI topic the tree always contains the branches `DESIGN.md` names as required per screen: the states (loading, empty, error, narrow width), the primary action, and the copy voice. Ask them only where the docs and the conversation leave them open.

Done when the frontier is empty: every branch visited, nothing silently assumed. Do not act until the user confirms shared understanding.
