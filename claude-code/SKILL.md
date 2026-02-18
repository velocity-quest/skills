---
name: velocity
description: Manage issues, projects, and workspaces in Velocity via MCP. Use proactively during development to track progress, file bugs, update statuses, and comment on issues — not just when the user explicitly asks.
allowed-tools: Read, Grep, Bash
---

# Velocity MCP Skill

You have access to the Velocity project management MCP server. Use it **proactively** during development — not just when the user explicitly asks about issues or projects.

## Agentic Development Workflow

This is the core loop for how you should use Velocity while coding:

### 1. Orient — Understand the Workspace

Before doing any work, discover the workspace structure. Cache these results mentally for the session:

```
list_teams         → team IDs and prefixes (e.g. ENG, DES, OPS)
list_statuses      → workflow states per team (Backlog, Todo, In Progress, Done, Cancelled)
list_members       → who's on the team, their user IDs
list_labels        → available labels (bug, feature, improvement, etc.)
```

### 2. Pick Up Work — Find or Create Issues

**When the user asks you to work on something specific:**
```
get_issue(issueId: "ENG-42")              → get full context
list_comments(issueId: "...")              → read discussion history
update_issue(issueId: "...", statusId: "in_progress_id")  → mark In Progress
add_comment(issueId: "...", body: "Starting work on this. Plan: ...")
```

**When the user describes work without referencing an issue:**
```
search_issues(query: "the thing they described")  → check if it already exists
# If no match:
create_issue(title: "...", teamId: "...", priority: "...", description: "...")
# Then proceed with implementation
```

**When you discover a bug while working on something else:**
```
create_issue(
  title: "Bug: [what's broken]",
  teamId: "...",
  priority: "HIGH",
  description: "Found while working on ENG-42.\n\n## Steps to reproduce\n...\n\n## Expected vs actual\n...",
  labelIds: ["bug_label_id"]
)
add_comment(issueId: "ENG-42", body: "Found related bug, filed as ENG-45")
```

### 3. Work — Update Progress as You Go

As you implement, keep the issue updated:

```
# When you start
update_issue(issueId: "...", statusId: "in_progress_id")
add_comment(issueId: "...", body: "Starting implementation. Approach: ...")

# When you make significant progress or hit a decision point
add_comment(issueId: "...", body: "Implemented the data model. Moving to API layer next.")

# When you find something relevant
add_comment(issueId: "...", body: "Note: this also affects the billing module, may need follow-up.")

# When you're blocked or need input
add_comment(issueId: "...", body: "Blocked: need decision on whether to use WebSockets or SSE for real-time updates.")
```

### 4. Complete — Close Issues and File Follow-ups

```
# Mark done
update_issue(issueId: "...", statusId: "done_id")
add_comment(issueId: "...", body: "Completed. Changes:\n- Added X\n- Modified Y\n- Tests passing")

# If you identified follow-up work
create_issue(
  title: "Follow-up: [what needs doing next]",
  teamId: "...",
  priority: "MEDIUM",
  description: "Identified during work on ENG-42. ..."
)
```

### 5. Review — Triage and Manage

**Daily triage / sprint review:**
```
list_issues(priority: "URGENT")                    → what's on fire?
list_issues(assigneeId: "user_id")                 → what's on my plate?
list_cycles(status: "ACTIVE")                      → current sprint
list_issues(statusId: "in_progress_id")            → what's actively being worked on?
```

**Project status check:**
```
get_project(projectId: "...")                      → milestones, issue count, progress
list_issues(projectId: "...", statusId: "done_id") → what's completed
list_issues(projectId: "...", statusId: "todo_id") → what's remaining
```

## Issue Description Best Practices

When creating issues, write descriptions in **Markdown** — they render as rich text in the UI:

```markdown
## Summary
Brief description of what needs to happen.

## Context
Why this matters. Link related issues by identifier: see ENG-42.

## Acceptance Criteria
- [ ] First requirement
- [ ] Second requirement
- [ ] Tests pass

## Technical Notes
Implementation hints, relevant files, constraints.
```

For bugs:
```markdown
## Bug Report
What's broken and what impact it has.

## Steps to Reproduce
1. Go to...
2. Click...
3. Observe...

## Expected Behavior
What should happen.

## Actual Behavior
What happens instead.

## Environment
Browser, OS, relevant config.
```

## When to Use Velocity Proactively

**DO use it when:**
- Starting work on a task → create or update an issue to In Progress
- Finishing work → mark issue Done, add summary comment
- Finding a bug during development → file it immediately
- Making a decision → comment on the issue explaining your reasoning
- The user asks what's left / what's next → query issues and summarize
- You need context about existing work → search and read issues + comments

**DON'T wait for the user to explicitly say "create an issue" or "update the status."** If you're doing development work and there's an issue to track it, keep it updated. If there isn't an issue, consider creating one.

## Tool Reference

### Issue Tracking (7 tools)
| Tool | Required | Optional |
|------|----------|----------|
| `list_issues` | — | `projectId`, `statusId`, `priority`, `assigneeId`, `labelId`, `limit`, `offset` |
| `get_issue` | `issueId` | — |
| `create_issue` | `title`, `teamId` | `description`, `priority`, `statusId`, `assigneeId`, `labelIds`, `projectId` |
| `update_issue` | `issueId` | `title`, `description`, `priority`, `statusId`, `assigneeId` |
| `search_issues` | `query` | `limit` |
| `add_comment` | `issueId`, `body` | `parentId` |
| `list_comments` | `issueId` | — |

### Projects & Cycles (4 tools)
| Tool | Required | Optional |
|------|----------|----------|
| `list_projects` | — | `status` (BACKLOG/PLANNED/IN_PROGRESS/COMPLETED/CANCELLED) |
| `get_project` | `projectId` | — |
| `list_cycles` | — | `status` (UPCOMING/ACTIVE/COMPLETED) |
| `get_cycle` | `id` | — |

### Workspace Metadata (4 tools)
| Tool | Required | Optional |
|------|----------|----------|
| `list_teams` | — | — |
| `list_labels` | — | — |
| `list_statuses` | — | — |
| `list_members` | — | — |

### Roadmap (9 tools)
| Tool | Required | Optional |
|------|----------|----------|
| `list_roadmap_items` | — | `status`, `category`, `versionId`, `limit` |
| `create_roadmap_item` | `title` | `description`, `status`, `category`, `versionId`, `assigneeId`, `isPublic` |
| `update_roadmap_item` | `id` | `title`, `description`, `status`, `category`, `versionId`, `assigneeId`, `isPublic` |
| `delete_roadmap_item` | `id` | — |
| `vote_roadmap_item` | `id` | — |
| `list_roadmap_versions` | — | — |
| `create_roadmap_version` | `name` | `description`, `targetDate` |
| `get_roadmap_settings` | — | — |
| `update_roadmap_settings` | — | `isPublicEnabled`, `allowSubmissions`, `allowVoting` |

### Workspace & User (10 tools)
| Tool | Required | Optional |
|------|----------|----------|
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

### Custom Domains (4 tools)
| Tool | Required | Optional |
|------|----------|----------|
| `list_domains` | — | — |
| `add_domain` | `domain` | — |
| `verify_domain` | `id` | — |
| `remove_domain` | `id` | — |

## Key Concepts

- **Identifiers**: Issues use team-prefixed identifiers like `ENG-42`. Always prefer these over UUIDs when talking to the user.
- **Priority**: URGENT, HIGH, MEDIUM, LOW, NONE.
- **Statuses**: Workspace-specific. Always call `list_statuses` to discover the exact names and IDs. Common groups: backlog, unstarted, started (In Progress), completed (Done), cancelled.
- **Labels**: Workspace-specific categorization (bug, feature, improvement, etc.). Discover with `list_labels`.
- **Projects**: Groups of related issues with milestones. Issues can belong to one project.
- **Cycles**: Time-boxed sprints. Issues can be assigned to a cycle.
