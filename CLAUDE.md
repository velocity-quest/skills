# Velocity MCP Server

You have access to the Velocity project management MCP server at `https://velocity.quest/api/mcp`. Use it to manage issues, projects, roadmaps, workspaces, and more.

## Read Tools

### Issue Tracking
- `list_issues` — List issues. Supports filters: `projectId`, `statusId`, `priority`, `assigneeId`, `labelId`. Supports `limit`/`offset` pagination.
- `get_issue` — Get a single issue by UUID or identifier (e.g. `ENG-42`).
- `search_issues` — Full-text search across issue titles, descriptions, and identifiers.
- `list_comments` — List all comments on an issue.

### Projects & Cycles
- `list_projects` — List all projects. Supports `status` filter (BACKLOG, PLANNED, IN_PROGRESS, COMPLETED, CANCELLED).
- `get_project` — Get project details including milestones and issue count.
- `list_cycles` — List cycles (sprints). Supports `status` filter (UPCOMING, ACTIVE, COMPLETED).
- `get_cycle` — Get cycle details with issue counts and progress.

### Workspace Metadata
- `list_teams` — List all teams. Call this first to discover team IDs.
- `list_labels` — List available labels.
- `list_statuses` — List workflow statuses across all teams.
- `list_members` — List workspace members with roles.

### Roadmap
- `list_roadmap_items` — List roadmap items with status, category, and version filters.
- `list_roadmap_versions` — List all roadmap versions (releases).
- `get_roadmap_settings` — Get roadmap visibility and voting settings.

### Workspace & User
- `list_workspaces` — List all workspaces the user belongs to.
- `get_workspace` — Get current workspace details (name, slug, plan, member/team counts).
- `get_current_user` — Get the authenticated user's profile.
- `list_user_api_keys` — List personal API keys (`velu_` prefix).

### Custom Domains
- `list_domains` — List custom domains with verification status.

## Write Tools

### Issue Tracking
- `create_issue` — Create a new issue. Required: `title`, `teamId`. Optional: `description`, `priority` (URGENT/HIGH/MEDIUM/LOW/NONE), `statusId`, `assigneeId`, `labelIds`, `projectId`.
- `update_issue` — Update an issue by UUID. Any field can be updated.
- `add_comment` — Add a comment to an issue. Supports threaded replies via `parentId`.

### Roadmap
- `create_roadmap_item` — Create a roadmap item with title, status, category, version.
- `update_roadmap_item` — Update a roadmap item.
- `delete_roadmap_item` — Delete a roadmap item.
- `vote_roadmap_item` — Toggle vote on a roadmap item.
- `create_roadmap_version` — Create a new roadmap version (release milestone).
- `update_roadmap_settings` — Update roadmap visibility and voting settings.

### Workspace & User
- `create_workspace` — Create a new workspace. Required: `name`, `slug`. User becomes owner.
- `update_workspace` — Update workspace name or description.
- `delete_workspace` — Permanently delete a workspace (owner only).
- `update_current_user` — Update user display name or avatar.
- `create_user_api_key` — Create a personal API key. Required: `name`, `scopes`. Key returned once.
- `revoke_user_api_key` — Revoke a personal API key by ID.

### Custom Domains
- `add_domain` — Add a custom domain. Returns DNS setup instructions.
- `verify_domain` — Trigger domain verification.
- `remove_domain` — Remove a custom domain.

## Workflow Tips

1. **Start with `list_teams`** to discover available teams and their IDs before creating or querying issues.
2. **Use identifiers** (e.g. `ENG-42`) when referencing issues — they are human-readable and stable.
3. **Check for duplicates** with `search_issues` or `list_issues` before creating new issues.
4. **Priority levels**: URGENT, HIGH, MEDIUM, LOW, NONE.
5. **Status names** are workspace-specific. Use `list_statuses` to get the exact names and IDs.
6. When the user says "file a bug" or "create a ticket", use `create_issue`.
7. When the user asks "what am I working on?", use `list_issues` filtered by their assignee ID.
8. Use `list_workspaces` to discover workspaces, `create_workspace` to set up new ones.
