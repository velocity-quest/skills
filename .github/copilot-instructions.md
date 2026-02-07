# Velocity Project Management

You have access to the Velocity MCP server for project management. Use it when the user mentions issues, bugs, tasks, projects, sprints, cycles, or team workload.

## Key Concepts

- **Teams** — Organizational units (e.g. Engineering, Design). Each team has its own issue prefix.
- **Issues** — Work items identified by team-prefixed identifiers like `ENG-42`. Have a title, description, priority (0-4), status, assignee, and labels.
- **Projects** — Groups of related issues with milestones and progress tracking.
- **Cycles** — Time-boxed sprints. Can be `active`, `upcoming`, or `completed`.
- **Labels** — Categorization tags (e.g. `bug`, `feature`, `improvement`).

## Workflow Tips

1. Call `list_teams` first to discover team IDs before other operations.
2. Use `search` or `list_issues` to check for duplicates before creating issues.
3. Use human-readable identifiers (`ENG-42`) rather than UUIDs.
4. Priority levels: 0 = None, 1 = Urgent, 2 = High, 3 = Medium, 4 = Low.
5. Call `list_statuses` to learn the exact workflow status names for the workspace.
