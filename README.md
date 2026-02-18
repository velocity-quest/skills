# Velocity Skills

AI coding agent skills and instructions for [Velocity](https://velocity.quest) — the project management platform with a built-in MCP server.

## What is this?

This repository contains instruction files that teach AI coding agents how to use the Velocity MCP server **proactively during development** — not just when explicitly asked. Drop these files into your project, and your agent will automatically track its work: picking up issues, updating progress, filing bugs, and marking tasks complete.

## Prerequisites

- A Velocity workspace on the **Pro** plan or above
- An MCP connection token (create one at **Settings > MCP Server**)

## Setup

### Claude Code

Add to `.mcp.json` in your project root:

```json
{
  "mcpServers": {
    "velocity": {
      "url": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "velocity": {
      "url": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "velocity": {
      "serverUrl": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

### Gemini CLI

Add to `.gemini/settings.json` in your project root:

```json
{
  "mcpServers": {
    "velocity": {
      "url": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

### OpenCode

Add to `.opencode.json` in your project root:

```json
{
  "mcp": {
    "velocity": {
      "type": "remote",
      "url": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json` in your project root:

```json
{
  "servers": {
    "velocity": {
      "type": "http",
      "url": "https://velocity.quest/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN_HERE"
      }
    }
  }
}
```

## How Agents Use Velocity

Once connected, agents follow an **agentic development workflow**:

1. **Orient** — Call `list_teams`, `list_statuses`, `list_labels` to understand the workspace
2. **Pick up work** — `get_issue("ENG-42")` to read context, `update_issue` to mark In Progress
3. **Track progress** — `add_comment` as they implement, noting decisions and blockers
4. **Complete** — `update_issue` to mark Done, `add_comment` with a summary of changes
5. **File follow-ups** — `create_issue` for bugs discovered or work identified during implementation

Agents are instructed to use these tools **proactively** — they don't wait for the user to say "create an issue" or "update the status."

## Available MCP Tools (38)

### Issue Tracking (7 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_issues` | List issues with filtering and pagination | read |
| `get_issue` | Get full issue details by UUID or identifier (e.g. `ENG-42`) | read |
| `create_issue` | Create a new issue | write |
| `update_issue` | Update an existing issue | write |
| `search_issues` | Full-text search across issues | read |
| `add_comment` | Add a comment to an issue (supports threaded replies) | write |
| `list_comments` | List all comments on an issue | read |

### Projects & Cycles (4 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_projects` | List projects with status filter | read |
| `get_project` | Get project details and milestones | read |
| `list_cycles` | List cycles (sprints) with status filter | read |
| `get_cycle` | Get cycle details and progress | read |

### Workspace Metadata (4 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_teams` | List all teams in the workspace | read |
| `list_labels` | List available labels | read |
| `list_statuses` | List workflow statuses per team | read |
| `list_members` | List workspace members | read |

### Roadmap (9 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_roadmap_items` | List roadmap items with filters | read |
| `create_roadmap_item` | Create a roadmap item | write |
| `update_roadmap_item` | Update a roadmap item | write |
| `delete_roadmap_item` | Delete a roadmap item | write |
| `vote_roadmap_item` | Toggle vote on a roadmap item | write |
| `list_roadmap_versions` | List roadmap versions (releases) | read |
| `create_roadmap_version` | Create a roadmap version | write |
| `get_roadmap_settings` | Get roadmap settings | read |
| `update_roadmap_settings` | Update roadmap settings | write |

### Workspace & User (10 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_workspaces` | List all workspaces the user belongs to | read |
| `create_workspace` | Create a new workspace (user becomes owner) | write |
| `delete_workspace` | Permanently delete a workspace (owner only) | write |
| `get_workspace` | Get current workspace details | read |
| `update_workspace` | Update workspace name or description | write |
| `get_current_user` | Get authenticated user's profile | read |
| `update_current_user` | Update user display name or avatar | write |
| `list_user_api_keys` | List personal API keys (`velu_` prefix) | read |
| `create_user_api_key` | Create a personal API key (returned once) | write |
| `revoke_user_api_key` | Revoke a personal API key | write |

### Custom Domains (4 tools)

| Tool | Description | Scope |
|------|-------------|-------|
| `list_domains` | List custom domains | read |
| `add_domain` | Add a custom domain | write |
| `verify_domain` | Verify domain DNS records | write |
| `remove_domain` | Remove a custom domain | write |

## Using the Skill Files

| File | Agent | Purpose |
|------|-------|---------|
| `CLAUDE.md` | Claude Code | Project instructions loaded automatically |
| `AGENTS.md` | Gemini CLI | Agent instructions loaded automatically |
| `claude-code/SKILL.md` | Claude Code | Installable skill with tool reference |
| `.github/copilot-instructions.md` | GitHub Copilot | Custom instructions for Copilot |

Copy any of these files into your project to give the respective agent context about Velocity's MCP tools and the agentic development workflow.

## License

MIT
