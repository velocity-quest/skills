# Velocity Skills

AI coding agent skills and instructions for [Velocity](https://velocity.quest) — the project management platform with a built-in MCP server.

## What is this?

This repository contains instruction files that AI coding agents can consume to understand how to interact with the Velocity MCP server. Drop these files into your project, and your agent will know how to create issues, query projects, manage cycles, and more — all without leaving your editor.

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

## Available MCP Tools

| Tool | Description | Required Scope |
|------|-------------|----------------|
| `list_teams` | List all teams in the workspace | `read:teams` |
| `get_team` | Get details for a specific team | `read:teams` |
| `list_issues` | List issues with filtering and pagination | `read:issues` |
| `get_issue` | Get full issue details by identifier | `read:issues` |
| `create_issue` | Create a new issue | `write:issues` |
| `update_issue` | Update an existing issue | `write:issues` |
| `list_projects` | List projects in the workspace | `read:projects` |
| `get_project` | Get project details and milestones | `read:projects` |
| `list_cycles` | List cycles (sprints) | `read:cycles` |
| `get_cycle` | Get cycle details and snapshot | `read:cycles` |
| `list_labels` | List available labels | `read:labels` |
| `list_statuses` | List workflow statuses | `read:statuses` |
| `list_members` | List workspace members | `read:members` |
| `search` | Search across issues, projects, and cycles | `read:issues` |
| `get_workspace` | Get workspace info and stats | `read:workspace` |

## Using the Skill Files

| File | Agent | Purpose |
|------|-------|---------|
| `CLAUDE.md` | Claude Code | Project instructions loaded automatically |
| `AGENTS.md` | Gemini CLI | Agent instructions loaded automatically |
| `claude-code/SKILL.md` | Claude Code | Installable skill with tool reference |
| `.github/copilot-instructions.md` | GitHub Copilot | Custom instructions for Copilot |

Copy any of these files into your project to give the respective agent context about Velocity's MCP tools.

## License

MIT
