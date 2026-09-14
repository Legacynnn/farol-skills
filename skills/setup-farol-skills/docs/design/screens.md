---
status: living
updated: <YYYY-MM-DD>
owner: shape-ui, finish-screen, sync-docs
---

# Screens

Every screen and shared surface, what it is for, and where it stands. The inventory agents use to find the host page for a prototype and to see which screens still lack a state.

## Shells

| Shell | Path | Used by |
| --- | --- | --- |
| <app shell> | <route or component> | <screens> |

## Screens

| Screen | Route | Purpose | Primary action | States done | Status | Spec | Brief |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <name> | <route> | <one line> | <verb> | `L E R N` | `planned | prototyped | built | finished` | <id> | <path> |

`L E R N` marks loading, empty, error, narrow width; a missing letter is a missing state.

## Shared surfaces

Components with product-level meaning (the command palette, the notification tray, the onboarding checklist), one row each in the same shape.

## Update triggers

- `shape-ui` writes a brief → row with status `planned`, brief path
- `prototype` picks a winner → `prototyped`, spec link to the verdict
- `implement` produces a screen → `built`, states as shipped
- `finish-screen` completes → `finished`, all four letters
- A route is renamed or removed → row updated or deleted, same commit

## Sources

_none yet_
