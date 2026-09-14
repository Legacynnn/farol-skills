# Issue tracker: GitHub

Specs and tickets live as GitHub Issues. Use `gh` for everything; it infers the repo from the clone.

- **Create**: `gh issue create --title "..." --body "..."` (heredoc for bodies)
- **Read**: `gh issue view <n> --comments`
- **List**: `gh issue list --state open --label ready-for-agent --json number,title,body,labels`
- **Comment / label / close**: `gh issue comment`, `gh issue edit --add-label`, `gh issue close`

## Publish a spec

One issue titled `Spec: <feature>`, label `spec`.

## Publish tickets

One issue per ticket in dependency order, label `ready-for-agent`, `Part of #<spec>` on the first line. Blocking edges via native issue dependencies (`gh api --method POST repos/<o>/<r>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker db id>`), falling back to a `Blocked by: #n` line when unavailable.

## Frontier

Open `ready-for-agent` issues with no open blockers and no assignee. `gh issue edit <n> --add-assignee @me` is the first write of a session.

## Notes

Explorations and prototypes live locally under `.scratch/explorations/` and `.scratch/prototypes/`; link from the issue.
