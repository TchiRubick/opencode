# OpenCode Configuration

Personal [OpenCode](https://opencode.ai/) AI configuration workspace.

## Overview

This repository contains the configuration files, custom prompts, and agent definitions for the OpenCode AI coding assistant. It defines multiple specialized agents for different workflows — from daily coding tasks to full Spec-Driven Development (SDD) lifecycle management.

## Repository Structure

```
.
├── opencode.json          # Main configuration — agents, MCP servers, permissions, plugins
├── tui.json               # Terminal UI keybinds and plugins
├── dcp.jsonc              # Dynamic Context Pruning (DCP) schema reference
├── AGENTS.md              # Engineering rules and behavior guidelines for all agents
├── README.md              # This file
│
├── prompts/               # Custom agent prompt files
│   ├── build-agent.md
│   ├── plan-agent.md
│   ├── plan-file-agent.md
│   └── sdd/
│       ├── sdd-orchestrator.md
│       ├── sdd-explore.md
│       ├── sdd-propose.md
│       ├── sdd-spec.md
│       ├── sdd-design.md
│       ├── sdd-tasks.md
│       ├── sdd-apply.md
│       ├── sdd-verify.md
│       ├── sdd-archive.md
│       ├── sdd-init.md
│       └── sdd-onboard.md
│
├── .env                   # Environment secrets (gitignored)
├── .everynotify.json      # Notification config (Slack webhook, etc.)
├── .gitignore             # Ignores node_modules, secrets, lockfiles
└── package.json           # Plugin dependencies
```

## Agents

| Agent | Mode | Purpose |
|-------|------|---------|
| `build` | Primary | Day-to-day coding, implementation, review, debugging |
| `plan` | Primary | High-level planning and analysis |
| `plan-file` | Subagent | Writes plans to planning documents |
| `gentle-orchestrator` | Primary | SDD workflow orchestration — coordinates explore → propose → spec → design → tasks → apply → verify → archive |
| `sdd-explore` | Subagent | Investigate codebase and clarify requirements |
| `sdd-propose` | Subagent | Create change proposals |
| `sdd-spec` | Subagent | Write detailed specifications |
| `sdd-design` | Subagent | Create technical designs |
| `sdd-tasks` | Subagent | Break down specs into implementation tasks |
| `sdd-apply` | Subagent | Implement code changes from tasks |
| `sdd-verify` | Subagent | Validate implementation against specs |
| `sdd-archive` | Subagent | Archive completed change artifacts |
| `sdd-init` | Subagent | Bootstrap SDD context in a project |
| `sdd-onboard` | Subagent | Guide users through a complete SDD cycle |

## MCP Servers

| Server | Type | Purpose |
|--------|------|---------|
| `Figma` | Local | Figma design integration via MCP proxy |
| `local-figma` | Local | Chrome DevTools integration for Figma |
| `context7` | Remote | Documentation and code search (requires `CONTEXT7_API_KEY`) |
| `engram` | Local | Persistent memory and context management |
| `playwright` | Local | Browser automation and testing |
| `browser-control` | Local | Browser control via extension |

## Plugins

- `@mohak34/opencode-notifier` — Desktop notifications
- `opencode-antigravity-auth` — Authentication management
- `@tarquinen/opencode-dcp` — Dynamic Context Pruning
- `@sillybit/opencode-plugin-everynotify` — Slack/webhook notifications
- `opencode-subagent-statusline` — Status line for subagents (TUI)
- `opencode-sdd-engram-manage` — Engram integration for SDD workflows

## Setup

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Configure secrets** in `.env`:
   ```bash
   CONTEXT7_API_KEY=your_key_here
   ```

3. **Optional: Configure notifications** in `.everynotify.json`:
   ```json
   {
     "slack": {
       "enabled": true,
       "webhookUrl": "https://hooks.slack.com/services/..."
     }
   }
   ```

## SDD Workflow

This configuration supports the full Spec-Driven Development lifecycle:

```
/sdd-init     → Bootstrap project context
/sdd-explore  → Investigate and clarify
/sdd-propose  → Create change proposal
/sdd-spec     → Write specifications
/sdd-design   → Create technical design
/sdd-tasks    → Break into tasks
/sdd-apply    → Implement
/sdd-verify   → Validate
/sdd-archive  → Archive completed work
```

The `gentle-orchestrator` agent coordinates this workflow and delegates to specialized sub-agents at each phase.

## Agent Behavior

All agents follow the engineering rules defined in [`AGENTS.md`](./AGENTS.md):

- Make the smallest correct change
- Follow existing project patterns
- Avoid unrelated refactors
- Do not expose secrets
- Verify technical claims against code/docs
- Results first, concise by default
- Use conventional commits

## License

Personal configuration — not intended for redistribution.
