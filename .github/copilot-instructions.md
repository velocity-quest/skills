# Velocity Project Management

You have access to the Velocity MCP server for project management. Use it when the user mentions issues, bugs, tasks, projects, sprints, cycles, roadmap, workspaces, or team workload.

## Key Concepts

- **Workspaces** — Top-level containers. Each has a unique URL slug, teams, and a billing plan. Create with `create_workspace`, list with `list_workspaces`.
- **Teams** — Organizational units (e.g. Engineering, Design). Each team has its own issue prefix.
- **Issues** — Work items identified by team-prefixed identifiers like `ENG-42`. Have a title, description, priority (URGENT/HIGH/MEDIUM/LOW/NONE), status, assignee, and labels.
- **Projects** — Groups of related issues with milestones and progress tracking.
- **Cycles** — Time-boxed sprints. Can be UPCOMING, ACTIVE, or COMPLETED.
- **Labels** — Categorization tags (e.g. `bug`, `feature`, `improvement`).
- **Roadmap** — Public-facing feature planning with items, versions, and voting.
- **Custom Domains** — User-configured domains with DNS verification.

## Workflow Tips

1. Call `list_teams` first to discover team IDs before other operations.
2. Use `search_issues` or `list_issues` to check for duplicates before creating issues.
3. Use human-readable identifiers (`ENG-42`) rather than UUIDs.
4. Priority levels: URGENT, HIGH, MEDIUM, LOW, NONE.
5. Call `list_statuses` to learn the exact workflow status names for the workspace.
6. Use `list_workspaces` to discover workspaces, `create_workspace` to create new ones.
7. Use `add_comment` for threaded discussions on issues.
8. Use roadmap tools (`list_roadmap_items`, `create_roadmap_item`, `vote_roadmap_item`) for feature planning.
