# Velocity MCP Server — Agent Instructions

You have access to the Velocity project management MCP server. Use it when the user asks about issues, bugs, tasks, projects, sprints, cycles, roadmap, workspaces, or team workload.

## Getting Started

1. Call `list_teams` to discover teams and their IDs.
2. Call `list_statuses` to learn the workflow status names and IDs.
3. Now you can create, query, and update issues.

## Common Workflows

### Create an Issue

```
1. list_teams → pick the right team
2. create_issue(title, teamId, priority?, assigneeId?, labelIds?)
```

### Find and Update an Issue

```
1. search_issues(query) OR get_issue(issueId: "ENG-42")
2. update_issue(issueId, fields...)
```

### List Issues by Priority

```
list_issues(priority: "URGENT")
list_issues(priority: "HIGH")
```

### Review a Project

```
1. get_project(projectId) → see milestones and progress
2. list_issues(projectId: id) → see all issues in the project
```

### Check Current Sprint

```
1. list_cycles(status: "ACTIVE") → get active cycle
2. list_issues filtered by cycle
```

### Manage Roadmap

```
1. list_roadmap_versions → find version
2. create_roadmap_item(title: "SSO Support", category: "FEATURE", versionId: "...")
3. vote_roadmap_item(id) → toggle vote
```

### Create a Workspace

```
create_workspace(name: "Acme Inc", slug: "acme-inc")
```

## Tool Reference

| Tool | Required Args | Optional Args |
|------|--------------|---------------|
| **Issue Tracking** | | |
| `list_issues` | — | `projectId`, `statusId`, `priority`, `assigneeId`, `labelId`, `limit`, `offset` |
| `get_issue` | `issueId` | — |
| `create_issue` | `title`, `teamId` | `description`, `priority`, `statusId`, `assigneeId`, `labelIds`, `projectId` |
| `update_issue` | `issueId` | `title`, `description`, `priority`, `statusId`, `assigneeId` |
| `search_issues` | `query` | `limit` |
| `add_comment` | `issueId`, `body` | `parentId` |
| `list_comments` | `issueId` | — |
| **Projects & Cycles** | | |
| `list_projects` | — | `status` |
| `get_project` | `projectId` | — |
| `list_cycles` | — | `status` |
| `get_cycle` | `id` | — |
| **Workspace Metadata** | | |
| `list_teams` | — | — |
| `list_labels` | — | — |
| `list_statuses` | — | — |
| `list_members` | — | — |
| **Roadmap** | | |
| `list_roadmap_items` | — | `status`, `category`, `versionId`, `limit` |
| `create_roadmap_item` | `title` | `description`, `status`, `category`, `versionId`, `assigneeId`, `isPublic` |
| `update_roadmap_item` | `id` | `title`, `description`, `status`, `category`, `versionId`, `assigneeId`, `isPublic` |
| `delete_roadmap_item` | `id` | — |
| `vote_roadmap_item` | `id` | — |
| `list_roadmap_versions` | — | — |
| `create_roadmap_version` | `name` | `description`, `targetDate` |
| `get_roadmap_settings` | — | — |
| `update_roadmap_settings` | — | `isPublicEnabled`, `allowSubmissions`, `allowVoting` |
| **Workspace & User** | | |
| `list_workspaces` | — | — |
| `create_workspace` | `name`, `slug` | `logoUrl` |
| `delete_workspace` | `id` | — |
| `get_workspace` | — | — |
| `update_workspace` | — | `name`, `description` |
| `get_current_user` | — | — |
| `update_current_user` | — | `displayName`, `avatarUrl` |
| `list_user_api_keys` | — | — |
| `create_user_api_key` | `name`, `scopes` | — |
| `revoke_user_api_key` | `id` | — |
| **Custom Domains** | | |
| `list_domains` | — | — |
| `add_domain` | `domain` | — |
| `verify_domain` | `id` | — |
| `remove_domain` | `id` | — |

## Priority Levels

| Value | Label |
|-------|-------|
| URGENT | Urgent |
| HIGH | High |
| MEDIUM | Medium |
| LOW | Low |
| NONE | No priority |
