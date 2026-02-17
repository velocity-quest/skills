---
name: velocity
description: Manage issues, projects, roadmaps, workspaces, and more in Velocity via MCP. Use when the user asks about issues, bugs, tasks, projects, sprints, roadmap, domains, or team workload.
allowed-tools: Read, Grep, Bash
---

# Velocity MCP Skill

Use the Velocity MCP tools to interact with the user's project management workspace.

## MCP Tool Reference

### Issue Tracking

- **list_issues**(projectId?, statusId?, priority?, assigneeId?, labelId?, limit?, offset?) — List issues with filters and pagination.
- **get_issue**(issueId) — Get full issue details by UUID or identifier (e.g. `ENG-42`).
- **create_issue**(title, teamId, description?, priority?, statusId?, assigneeId?, labelIds?, projectId?) — Create a new issue.
- **update_issue**(issueId, title?, description?, priority?, statusId?, assigneeId?) — Update an existing issue.
- **search_issues**(query, limit?) — Full-text search across issue titles, descriptions, and identifiers.
- **add_comment**(issueId, body, parentId?) — Add a comment to an issue.
- **list_comments**(issueId) — List all comments on an issue.

### Projects & Cycles

- **list_projects**(status?) — List all projects. Status: BACKLOG, PLANNED, IN_PROGRESS, COMPLETED, CANCELLED.
- **get_project**(projectId) — Get project details with milestones and issue count.
- **list_cycles**(status?) — List sprint cycles. Status: UPCOMING, ACTIVE, COMPLETED.
- **get_cycle**(id) — Get cycle details with issue counts and progress.

### Workspace Metadata

- **list_teams** — List all teams. Call first to get team IDs.
- **list_labels** — List available labels.
- **list_statuses** — List all workflow statuses across teams.
- **list_members** — List workspace members with roles.

### Roadmap

- **list_roadmap_items**(status?, category?, versionId?, limit?) — List roadmap items with filters.
- **create_roadmap_item**(title, description?, status?, category?, versionId?, assigneeId?, isPublic?) — Create a roadmap item.
- **update_roadmap_item**(id, title?, description?, status?, category?, versionId?, assigneeId?, isPublic?) — Update a roadmap item.
- **delete_roadmap_item**(id) — Delete a roadmap item.
- **vote_roadmap_item**(id) — Toggle vote on a roadmap item.
- **list_roadmap_versions** — List all roadmap versions (releases).
- **create_roadmap_version**(name, description?, targetDate?) — Create a new roadmap version.
- **get_roadmap_settings** — Get roadmap visibility and voting settings.
- **update_roadmap_settings**(isPublicEnabled?, allowSubmissions?, allowVoting?) — Update roadmap settings.

### Workspace & User

- **list_workspaces** — List all workspaces the user belongs to.
- **create_workspace**(name, slug, logoUrl?) — Create a new workspace (user becomes owner).
- **delete_workspace**(id) — Permanently delete a workspace (owner only).
- **get_workspace** — Get current workspace details (name, slug, plan, member/team counts).
- **update_workspace**(name?, description?) — Update workspace name or description.
- **get_current_user** — Get the authenticated user's profile.
- **update_current_user**(displayName?, avatarUrl?) — Update user display name or avatar.
- **list_user_api_keys** — List personal API keys (`velu_` prefix).
- **create_user_api_key**(name, scopes) — Create a personal API key (returned once).
- **revoke_user_api_key**(id) — Revoke a personal API key.

### Custom Domains

- **list_domains** — List custom domains with verification status.
- **add_domain**(domain) — Add a custom domain with DNS setup instructions.
- **verify_domain**(id) — Check domain verification status.
- **remove_domain**(id) — Remove a custom domain.

## Priority Levels

| Value | Label |
|-------|-------|
| URGENT | Urgent |
| HIGH | High |
| MEDIUM | Medium |
| LOW | Low |
| NONE | No priority |

## Identifier Format

Issues use team-prefixed identifiers like `ENG-42`, `DES-7`. Always prefer identifiers over UUIDs when communicating with the user.

## Example Workflows

### File a bug

```
1. list_teams → find the right team
2. create_issue(title: "Bug: ...", teamId: "...", priority: "HIGH")
```

### What's assigned to me?

```
1. list_members → find user's member ID
2. list_issues(assigneeId: "...")
```

### Move an issue to Done

```
1. list_statuses → find the "Done" status ID
2. update_issue(issueId: "...", statusId: "...")
```

### Search for related issues

```
search_issues(query: "authentication timeout")
```

### Create a workspace

```
create_workspace(name: "Acme Inc", slug: "acme-inc")
```

### Add a roadmap item

```
1. list_roadmap_versions → find version ID
2. create_roadmap_item(title: "SSO Support", category: "FEATURE", versionId: "...")
```
