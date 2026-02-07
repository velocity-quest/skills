# Velocity MCP Server

You have access to the Velocity project management MCP server at `https://velocity.quest/api/mcp`. Use it to manage issues, projects, cycles, and teams in the user's workspace.

## Read Tools

- `list_teams` — List all teams. Call this first to discover team IDs.
- `get_team` — Get team details by ID.
- `list_issues` — List issues. Supports filters: `teamId`, `status`, `priority`, `assigneeId`, `labelIds`, `projectId`, `cycleId`. Supports `first`/`after` pagination.
- `get_issue` — Get a single issue by its identifier (e.g. `ENG-42`).
- `list_projects` — List all projects. Supports `status` filter.
- `get_project` — Get project details including milestones.
- `list_cycles` — List cycles (sprints). Supports `status` filter (`active`, `upcoming`, `completed`).
- `get_cycle` — Get cycle details and progress snapshot.
- `list_labels` — List available labels.
- `list_statuses` — List workflow statuses (Backlog, Todo, In Progress, Done, Cancelled).
- `list_members` — List workspace members with roles.
- `search` — Full-text search across issues, projects, and cycles.
- `get_workspace` — Get workspace info and stats.

## Write Tools

- `create_issue` — Create a new issue. Required: `title`, `teamId`. Optional: `description`, `priority` (0-4), `status`, `assigneeId`, `labelIds`, `projectId`, `cycleId`.
- `update_issue` — Update an issue by identifier. Any field from create_issue can be updated.

## Workflow Tips

1. **Start with `list_teams`** to discover available teams and their IDs before creating or querying issues.
2. **Use identifiers** (e.g. `ENG-42`) when referencing issues — they are human-readable and stable.
3. **Check for duplicates** with `search` or `list_issues` before creating new issues.
4. **Priority levels**: 0 = No priority, 1 = Urgent, 2 = High, 3 = Medium, 4 = Low.
5. **Status names** are workspace-specific. Use `list_statuses` to get the exact names.
6. When the user says "file a bug" or "create a ticket", use `create_issue`.
7. When the user asks "what am I working on?", use `list_issues` filtered by their assignee ID.
