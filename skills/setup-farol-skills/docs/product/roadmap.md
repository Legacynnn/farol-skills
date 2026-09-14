---
status: living
updated: <YYYY-MM-DD>
owner: to-spec, sync-docs
---

# Roadmap

Now, next, later. Items are specs or spec-sized ideas, never tickets. Order within a column is priority. Dates only on **Now**.

## Now

Being built. Each item points at its spec and its ticket frontier.

- **<Feature>**: <spec path or id>, <n>/<m> tickets done, target <YYYY-MM-DD>

## Next

Specced or ready to spec. Starts when a Now item ships.

- **<Feature>**: <spec or one-line problem>, why next: <reason>

## Later

Ideas with a problem attached. No commitment.

- **<Idea>**: <problem it solves>, from <source>

## Shipped

Most recent first. One line each, with the date and the spec.

- `<YYYY-MM-DD>` **<Feature>**: <spec>

## Dropped

What we decided not to do and why, so it is not reproposed.

- **<Idea>**: <reason>, decided <date>

## Update triggers

- `to-spec` publishes → item enters Next (or Now when work starts at once)
- `to-tickets` publishes → item moves to Now with its ticket count
- A ticket completes → update the Now count
- Last ticket done → move to Shipped with the date
- `grill-me` produces a problem without a spec → Later

## Sources

_none yet_
