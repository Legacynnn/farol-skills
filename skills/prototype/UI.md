# UI prototype

Several **structurally different** variants of one piece of UI, on one route, behind a fixed picker. The user flips, picks, steals bits from each, and the rest goes to the prototype branch.

Before building, call the Skill tool twice, for "better-ui" and "emil-design-eng". Every variant clears their bar individually: right easing, sub-300ms motion, transform/opacity only, concentric radii, shadows for depth, reduced motion honoured. Divergence is never an excuse to drop craft.

## Where it renders

Prefer **inside an existing page**: real header, real neighbours, real data density. A variant alone in a vacuum always looks fine. Mount variants on the existing route gated by `?variant=<name>`; keep the existing data fetching and swap only the rendered subtree. A piece with no page yet but a natural home (a new dashboard section, a new step in a flow) still mounts inside that host.

Only when nothing can host it: a throwaway route following the convention `docs/agents/navigation.md` names (default `/prototype/<name>`), with `prototype` in the path. No project at all: one self-contained HTML file.

## Process

### 1. Scope one piece and pick N

One piece per run. "The dashboard" is not a piece; the metric card is. Restate the brief in one line: what it is, where it renders, what it must do. Default 3 variants, cap 5.

### 2. Recon the ground

`DESIGN.md` is the source: tokens, type, radius, elevation, motion, voice, the states every screen ships with. Variants use its tokens and its component library; they should look shippable in this product tomorrow. Check `package.json` for the motion library before writing a spring.

### 3. Name the axis before code

Variants diverge on **one primary axis**, each at a different position:

| Axis | What varies |
| --- | --- |
| Structure | grouping, order, column count, what collapses |
| Density | spacing scale, hit areas, how much fits |
| Emphasis | where filled colour goes, what recedes |
| Interaction model | inline edit vs modal, progressive disclosure vs flat, drag vs buttons |
| Motion story | what moves and why, within the `DESIGN.md` budget |

Names describe the direction (`Quiet`, `Editorial`, `Dense`), never `A/B/C`. Two variants that differ only in colour or copy are one variant; replace one. Write the set down before building.

### 4. Build

One exported component per variant (`VariantQuiet`, …). A single switcher reads `?variant=` and renders exactly one, full size, with realistic content: product-shaped copy in the `DESIGN.md` voice, plausible names and numbers, the real row count. No lorem ipsum, no dead buttons; mutations go to stubs.

The picker is specified in [PICKER.md](PICKER.md), verbatim. It is harness chrome, not part of the design, so it never takes the project's tokens.

Every variant ships with the states `DESIGN.md` requires: loading, empty, error, narrow width. The picker's replay key re-mounts so entrances re-run.

### 5. Verify and hand over

Flip through every variant yourself: renders, interactions respond, console clean, 320px width holds. Screenshot each when browser tooling is available. Then present and **stop**:

| # | Variant | Axis position | When it wins | Its cost |
| --- | --- | --- | --- | --- |

Give the URL and the keys. The best feedback is "header from Quiet with the list from Dense": that is the design.

### 6. Capture and clean up

Record the verdict (which, why, what was stolen from where) in the spec, and any settled rule as one line in `DESIGN.md`'s Decisions log. Promote the winner through `/finish-screen`, which rewrites it to production standard. Move the losing variants and the switcher to the `prototype/<name>` branch. Main keeps only the winner.

## Anti-patterns

Variants that differ in tint. A shared `<Layout>` across variants. Real mutations. Promoting variant code straight to production. Judging at thumbnail size.
