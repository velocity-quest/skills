---
name: velocity
description: Manage issues, projects, and workspace data in Velocity via MCP. Use when the user asks about issues, bugs, tasks, projects, sprints, or team workload.
allowed-tools: Read, Grep, Bash
---

# Velocity MCP Skill

Use the Velocity MCP tools to interact with the user's project management workspace.

## MCP Tool Reference

### Read Operations

- **list_teams** — List all teams. Call first to get team IDs.
- **get_team**(id) — Team details.
- **list_issues**(teamId?, status?, priority?, assigneeId?, labelIds?, projectId?, cycleId?, first?, after?) — Query issues with filters.
- **get_issue**(identifier) — Single issue by identifier, e.g. `ENG-42`.
- **list_projects**(status?) — All projects.
- **get_project**(id) — Project details with milestones.
- **list_cycles**(status?) — Cycles/sprints. Status: `active`, `upcoming`, `completed`.
- **get_cycle**(id) — Cycle details and progress.
- **list_labels** — Available labels.
- **list_statuses** — Workflow statuses.
- **list_members** — Workspace members.
- **search**(query) — Full-text search across issues, projects, cycles.
- **get_workspace** — Workspace info and stats.

### Write Operations

- **create_issue**(title, teamId, description?, priority?, status?, assigneeId?, labelIds?, projectId?, cycleId?) — Create a new issue.
- **update_issue**(identifier, title?, description?, priority?, status?, assigneeId?, labelIds?, projectId?, cycleId?) — Update an existing issue.

## Priority Levels

| Value | Label |
|-------|-------|
| 0 | No priority |
| 1 | Urgent |
| 2 | High |
| 3 | Medium |
| 4 | Low |

## Identifier Format

Issues use team-prefixed identifiers like `ENG-42`, `DES-7`. Always prefer identifiers over UUIDs when communicating with the user.

## Example Workflows

### File a bug

```
1. list_teams → find the right team
2. create_issue(title: "Bug: ...", teamId: "...", priority: 2)
```

### What's assigned to me?

```
1. list_members → find user's member ID
2. list_issues(assigneeId: "...")
```

### Move an issue to Done

```
1. list_statuses → find the "Done" status name
2. update_issue(identifier: "ENG-42", status: "Done")
```

### Search for related issues

```
search(query: "authentication timeout")
```
