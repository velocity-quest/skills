# Velocity Project Management

You have access to the Velocity MCP server for project management. Use it **proactively** during development — not just when the user explicitly mentions issues or projects.

## Agentic Development Flow

### Starting Work

Before coding, orient yourself:

```
list_teams      → discover teams and their ID prefixes (ENG, DES, OPS)
list_statuses   → learn the workflow states (Backlog, Todo, In Progress, Done, Cancelled)
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
  description: "## Summary\n...\n\n## Steps to Reproduce\n1. ...\n\n## Expected\n...\n\n## Actual\n..."
)
```

Write descriptions in Markdown — they render as rich text in Velocity.

### Updating Progress

As you work, keep the issue updated with comments:

```
add_comment(issueId: "...", body: "Implemented the data model changes. Moving to API layer.")
add_comment(issueId: "...", body: "Found related issue — also affects billing. Filing follow-up.")
```

### Completing Work

```
update_issue(issueId: "...", statusId: "<done_status>")
add_comment(issueId: "...", body: "Done. Changes:\n- Added retry logic\n- Updated error handling\n- Tests passing")
```

If you identified follow-up work:
```
create_issue(title: "Follow-up: refactor token refresh logic", teamId: "...", priority: "MEDIUM",
  description: "Discovered during ENG-42. The token refresh path has duplicated logic.")
```

## Proactive Behaviors

**DO** use Velocity automatically when:
- Starting any development task → set issue to In Progress
- Finishing work → mark Done, add summary comment
- Discovering a bug → file it immediately, don't just mention it in chat
- Making a technical decision → comment on the issue with your reasoning
- Finding related issues → cross-reference with comments
- The user asks "what's left?" → query issues and give a real answer

**DON'T** wait for the user to say "create an issue" or "update the status." Track your work like a senior engineer would.

## Key Concepts

- **Workspaces** — Top-level containers. Each has a unique URL slug, teams, and a billing plan. Manage with `list_workspaces`, `create_workspace`, `delete_workspace`.
- **Teams** — Organizational units (e.g. Engineering, Design). Each team has its own issue prefix (ENG, DES).
- **Issues** — Work items identified by team-prefixed identifiers like `ENG-42`. Have a title, description, priority (URGENT/HIGH/MEDIUM/LOW/NONE), status, assignee, and labels.
- **Projects** — Groups of related issues with milestones and progress tracking.
- **Cycles** — Time-boxed sprints. Can be UPCOMING, ACTIVE, or COMPLETED.
- **Labels** — Categorization tags (e.g. `bug`, `feature`, `improvement`). Discover with `list_labels`.
- **Statuses** — Workspace-specific workflow states. Always call `list_statuses` to discover them.
- **Roadmap** — Public-facing feature planning with items, versions, and voting.
- **Custom Domains** — User-configured domains with DNS verification.

## Workflow Tips

1. Call `list_teams` and `list_statuses` first to discover IDs before other operations.
2. Use `search_issues` to check for duplicates before creating issues.
3. Use human-readable identifiers (`ENG-42`) rather than UUIDs.
4. Use `add_comment` for threaded discussions (supports `parentId` for replies).
5. Use roadmap tools for feature planning (`list_roadmap_items`, `create_roadmap_item`, `vote_roadmap_item`).
6. Personal API keys use the `velu_` prefix and work across all workspaces.
