# ADR format

ADRs live in `docs/adr/` as `0001-slug.md`, `0002-slug.md`. Scan for the highest number and increment.

```md
# {Short title of the decision}

{1-3 sentences: context, decision, why.}
```

One paragraph is a complete ADR. Optional, only when they add value: `Status` frontmatter (`proposed | accepted | deprecated | superseded by ADR-NNNN`), **Considered Options**, **Consequences**.

Offer an ADR only when all three hold:

1. **Hard to reverse.**
2. **Surprising without context.**
3. **A real trade-off** with genuine alternatives.

Qualifies: architectural shape, integration patterns between contexts, technology with lock-in, boundary and scope decisions, deliberate deviations from the obvious path, constraints invisible in code, non-obvious rejected alternatives.
