# CONTEXT.md format

```md
# {Context Name}

{One or two sentences: what this context is and why it exists.}

## Language

**Order**:
{One or two sentence definition.}
_Avoid_: Purchase, transaction

**Customer**:
A person or organization that places orders.
_Avoid_: Client, buyer, account
```

Rules:

- Be opinionated: one canonical word, the rest under `_Avoid_`.
- Definitions say what a thing IS, in one or two sentences.
- Only terms specific to this project's domain. General programming concepts stay out.
- Group under subheadings only when clusters emerge.

Multi-context repos carry a root `CONTEXT-MAP.md`:

```md
# Context Map

## Contexts

- [Ordering](./src/ordering/CONTEXT.md): receives and tracks orders
- [Billing](./src/billing/CONTEXT.md): invoices and payments

## Relationships

- **Ordering → Billing**: Ordering emits `OrderPlaced`; Billing consumes it
```
