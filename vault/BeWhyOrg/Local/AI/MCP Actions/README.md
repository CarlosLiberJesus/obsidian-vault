# Obsidian MCP Actions

This folder contains documentation and resources for the Obsidian MCP Actions system, which enables LLMs to interact with your Obsidian vault through the MCP server.

## Overview

The Obsidian MCP Actions system provides a structured approach for LLMs to:

1. Create and manage tasks in your daily notes
2. Create and update documentation in your vault
3. Log interactions and changes in the appropriate locations
4. Connect related information through links
5. Follow your established workflows and conventions

## Key Components

- **Task Management**: Uses the Obsidian Tasks plugin with your existing format
- **Documentation**: Creates and updates documentation in the appropriate locations
- **Logging**: Maintains logs of all actions in the Logs/Tasks folder
- **MCP Integration**: Provides API endpoints for LLMs to interact with your vault

## How It Works

1. An LLM connects to the MCP server
2. The LLM creates a task in your current daily note under ## Quick Add
3. The LLM creates a log file in Logs/Tasks with details of the action
4. The LLM performs the requested action (research, documentation, etc.)
5. The LLM updates the task status up to Testes [?]
6. You review the work and mark the task as complete when appropriate

## Task Format

Tasks follow your established format:

```
- [ ] priority ID description #task/area schedule_date due_date
```

Example:
```
- [ ] ⏫ MCP-001 Create documentation for API endpoints #task/mcp 📅 2025-04-10 ⏳ 2025-04-15
```

## Task Status Flow

LLMs will only progress tasks through these statuses:
- Action [ ] → Planeamento [B] → In Progress [d] → Testes [?]

Only humans should mark tasks as:
- Terminado [-] → Done [x]

## Folder Structure

```
vault/BeWhyOrg/Local/AI/MCP Actions/
├── README.md
├── API Documentation.md
├── Configuration Guide.md
├── Task Management.md
└── Examples/
    └── Example Task.md
```

## Logs Structure

```
vault/Logs/
├── Daily Logs/
│   └── YYYY-MM-DD.md (Contains tasks)
└── Tasks/
    └── MCP-XXX-Task-Name.md (Contains detailed logs)
```

## Getting Started

1. Review the [Configuration Guide](Configuration%20Guide.md) to set up the MCP server
2. Check the [Task Management](Task%20Management.md) document for details on how tasks are created and managed
3. See the [API Documentation](API%20Documentation.md) for information on the available API endpoints
4. Look at the [Examples](Examples/) folder for examples of how the system works
