# Issue tracker: Linear

Specs and tickets live in Linear. Use the Linear MCP tools (`mcp__linear-server__*`).

- **Team**: `<TEAM_KEY>`
- **Project**: `<project name or "per feature">`
- **Spec issue label**: `spec`
- **Ticket label**: `ready-for-agent`

## Publish a spec

Create one issue titled `Spec: <feature>` with the spec body as description, label `spec`. Record its identifier; tickets link to it.

## Publish tickets

One issue per ticket, created in dependency order so blockers have identifiers. Set the spec issue as parent. Use Linear's native **blocked by** relation for edges. Label `ready-for-agent`. Do not close or edit the parent.

## Fetch a ticket

`get_issue` by identifier (`ABC-123`) or URL, including comments and the parent spec.

## Frontier

`list_issues` filtered by label `ready-for-agent`, state unstarted, no open blockers, no assignee. Assign yourself before work. Move to `In Progress` on start, `Done` on merge.

## Notes

Explorations and prototypes still live locally under `.scratch/explorations/` and `.scratch/prototypes/`; link to them from the Linear issue rather than pasting them in.
