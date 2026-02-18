# Velocity MCP Server

You have access to the Velocity project management MCP server at `https://velocity.quest/api/mcp`. Use it **proactively** during development to track your work, file bugs, update issue statuses, and add comments — not just when the user explicitly asks.

## Agentic Development Flow

### Starting a Session

Before doing any work, orient yourself in the workspace:

```
list_teams      → discover teams and their ID prefixes (ENG, DES, OPS)
list_statuses   → learn the workflow states (Backlog, Todo, In Progress, Done, Cancelled)
list_members    → know who's on the team
list_labels     → available categorization tags (bug, feature, etc.)
```

### Picking Up an Issue

When the user asks you to work on `ENG-42` or describes something that maps to an existing issue:

```
get_issue(issueId: "ENG-42")                                    → read full context
list_comments(issueId: "...")                                    → read discussion history
update_issue(issueId: "...", statusId: "<in_progress_status>")   → mark In Progress
add_comment(issueId: "...", body: "Starting work. Plan: ...")    → log your approach
```

### Creating a New Issue

When the user describes work that doesn't have an issue yet, or you discover a bug:

```
search_issues(query: "...")    → check for duplicates first
create_issue(
  title: "Bug: login fails with expired token",
  teamId: "...",
  priority: "HIGH",
  description: "## Summary\n...\n\n## Steps to Reproduce\n1. ...\n\n## Expected\n...\n\n## Actual\n...",
  labelIds: ["<bug_label_id>"]
)
```

Write descriptions in Markdown — they render as rich text in Velocity.

### Updating Progress

As you work, keep the issue updated with comments:

```
add_comment(issueId: "...", body: "Implemented the data model changes. Moving to API layer.")
add_comment(issueId: "...", body: "Found related issue — also affects billing. Filing follow-up.")
add_comment(issueId: "...", body: "Blocked: need clarification on the auth flow before proceeding.")
```

### Completing Work

```
update_issue(issueId: "...", statusId: "<done_status>")
add_comment(issueId: "...", body: "Done. Changes:\n- Added retry logic to auth\n- Updated error handling in API\n- Tests passing")
```

If you identified follow-up work:
```
create_issue(title: "Follow-up: refactor token refresh logic", teamId: "...", priority: "MEDIUM",
  description: "Discovered during ENG-42. The token refresh path has duplicated logic that should be consolidated.")
```

### Proactive Behaviors

**DO** use Velocity automatically when:
- Starting any development task → set issue to In Progress
- Finishing work → mark Done, add summary comment
- Discovering a bug → file it immediately, don't just mention it in chat
- Making a technical decision → comment on the issue with your reasoning
- Finding related issues → cross-reference with comments
- The user asks "what's left?" → query issues and give a real answer

**DON'T** wait for the user to say "create an issue" or "update the status." Track your work like a senior engineer would.

## All Tools (38)

### Issue Tracking
- `list_issues` — List/filter issues. Filters: `projectId`, `statusId`, `priority` (URGENT/HIGH/MEDIUM/LOW/NONE), `assigneeId`, `labelId`. Pagination: `limit`, `offset`.
- `get_issue` — Get issue by UUID or identifier (e.g. `ENG-42`).
- `create_issue` — Create issue. Required: `title`, `teamId`. Optional: `description`, `priority`, `statusId`, `assigneeId`, `labelIds`, `projectId`.
- `update_issue` — Update issue. Required: `issueId`. Optional: `title`, `description`, `priority`, `statusId`, `assigneeId`.
- `search_issues` — Full-text search across titles, descriptions, identifiers. Required: `query`. Optional: `limit`.
- `add_comment` — Comment on an issue. Required: `issueId`, `body`. Optional: `parentId` (for threaded replies).
- `list_comments` — List all comments on an issue. Required: `issueId`.

### Projects & Cycles
- `list_projects` — List projects. Filter: `status` (BACKLOG/PLANNED/IN_PROGRESS/COMPLETED/CANCELLED).
- `get_project` — Project details with milestones and issue count. Required: `projectId`.
- `list_cycles` — List sprints. Filter: `status` (UPCOMING/ACTIVE/COMPLETED).
- `get_cycle` — Cycle details with issue counts and progress. Required: `id`.

### Workspace Metadata
- `list_teams` — All teams. **Call first** to discover team IDs.
- `list_labels` — All labels.
- `list_statuses` — All workflow statuses per team. **Call early** to learn status IDs.
- `list_members` — All workspace members with roles.

### Roadmap
- `list_roadmap_items` — List items. Filters: `status`, `category` (FEATURE/IMPROVEMENT/BUG/INFRASTRUCTURE), `versionId`, `limit`.
- `create_roadmap_item` — Required: `title`. Optional: `description`, `status`, `category`, `versionId`, `assigneeId`, `isPublic`.
- `update_roadmap_item` — Required: `id`. Same optional fields as create.
- `delete_roadmap_item` — Required: `id`.
- `vote_roadmap_item` — Toggle vote. Required: `id`.
- `list_roadmap_versions` — All versions (releases).
- `create_roadmap_version` — Required: `name`. Optional: `description`, `targetDate`.
- `get_roadmap_settings` — Visibility and voting settings.
- `update_roadmap_settings` — Optional: `isPublicEnabled`, `allowSubmissions`, `allowVoting`.

### Workspace & User
- `list_workspaces` — All workspaces the user belongs to.
- `create_workspace` — Required: `name`, `slug`. Optional: `logoUrl`. User becomes owner.
- `delete_workspace` — Required: `id`. Owner only.
- `get_workspace` — Current workspace details (name, slug, plan, counts).
- `update_workspace` — Optional: `name`, `description`.
- `get_current_user` — Authenticated user's profile.
- `update_current_user` — Optional: `displayName`, `avatarUrl`.
- `list_user_api_keys` — Personal API keys (`velu_` prefix).
- `create_user_api_key` — Required: `name`, `scopes`. Key returned once.
- `revoke_user_api_key` — Required: `id`.

### Custom Domains
- `list_domains` — All custom domains with verification status.
- `add_domain` — Required: `domain`. Returns DNS setup instructions.
- `verify_domain` — Required: `id`.
- `remove_domain` — Required: `id`.
