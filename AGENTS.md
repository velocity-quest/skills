# Velocity MCP Server — Agent Instructions

You have access to the Velocity project management MCP server. Use it when the user asks about issues, bugs, tasks, projects, sprints, cycles, or team workload.

## Getting Started

1. Call `list_teams` to discover teams and their IDs.
2. Call `list_statuses` to learn the workflow status names.
3. Now you can create, query, and update issues.

## Common Workflows

### Create an Issue

```
1. list_teams → pick the right team
2. create_issue(title, teamId, priority?, assigneeId?, labelIds?)
```

### Find and Update an Issue

```
1. search(query) OR get_issue(identifier: "ENG-42")
2. update_issue(identifier, fields...)
```

### List Issues by Priority

```
list_issues(teamId, priority: 1)   # Urgent
list_issues(teamId, priority: 2)   # High
```

### Review a Project

```
1. get_project(id) → see milestones and progress
2. list_issues(projectId: id) → see all issues in the project
```

### Check Current Sprint

```
1. list_cycles(status: "active") → get active cycle
2. list_issues(cycleId: id) → see sprint backlog
```

## Tool Reference

| Tool | Required Args | Optional Args |
|------|--------------|---------------|
| `list_teams` | — | — |
| `get_team` | `id` | — |
| `list_issues` | — | `teamId`, `status`, `priority`, `assigneeId`, `labelIds`, `projectId`, `cycleId`, `first`, `after` |
| `get_issue` | `identifier` | — |
| `create_issue` | `title`, `teamId` | `description`, `priority`, `status`, `assigneeId`, `labelIds`, `projectId`, `cycleId` |
| `update_issue` | `identifier` | `title`, `description`, `priority`, `status`, `assigneeId`, `labelIds`, `projectId`, `cycleId` |
| `list_projects` | — | `status` |
| `get_project` | `id` | — |
| `list_cycles` | — | `status` |
| `get_cycle` | `id` | — |
| `list_labels` | — | — |
| `list_statuses` | — | — |
| `list_members` | — | — |
| `search` | `query` | — |
| `get_workspace` | — | — |

## Priority Levels

| Value | Label |
|-------|-------|
| 0 | No priority |
| 1 | Urgent |
| 2 | High |
| 3 | Medium |
| 4 | Low |
