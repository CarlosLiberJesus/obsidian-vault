# Task Management

This document explains how tasks are created and managed in the Obsidian MCP Actions system.

## Task Format

Tasks follow your established format:

```
- [ ] priority ID description #task/area schedule_date due_date
```

Where:
- `priority` is one of: ⏫ (high), 🔼 (medium), normal (no symbol), ⏬ (low)
- `ID` is a unique identifier for the task (e.g., MCP-001)
- `description` is a brief description of the task
- `#task/area` is a tag that categorizes the task (e.g., #task/mcp, #task/documentation)
- `schedule_date` is when the task is scheduled to be worked on (📅 YYYY-MM-DD)
- `due_date` is when the task is due to be completed (⏳ YYYY-MM-DD)

Example:
```
- [ ] ⏫ MCP-001 Create documentation for API endpoints #task/mcp 📅 2025-04-10 ⏳ 2025-04-15
```

## Task Status Flow

Tasks progress through the following statuses:

1. **Action [ ]**: Initial status when a task is created
2. **Planeamento [B]**: Planning phase, when the task is being planned
3. **In Progress [d]**: Implementation phase, when the task is being worked on
4. **Testes [?]**: Testing phase, when the task is being tested
5. **Terminado [-]**: Completed phase, when the task is finished but not yet reviewed
6. **Done [x]**: Final status when a task is completed and reviewed

**Important**: LLMs should only progress tasks through statuses 1-4. Only humans should mark tasks as Terminado [-] or Done [x].

## Task Creation Process

When an LLM needs to create a task:

1. It generates a unique ID for the task (e.g., MCP-001)
2. It adds the task to the current daily note under the ## Quick Add section
3. It creates a log file in the Logs/Tasks folder with the same ID
4. It links the task to the log file using the ID

Example task in daily note:
```markdown
## Quick Add

- [ ] ⏫ MCP-001 Create documentation for API endpoints #task/mcp 📅 2025-04-10 ⏳ 2025-04-15
```

Example log file (Logs/Tasks/MCP-001-Create-documentation-for-API-endpoints.md):
```markdown
# MCP-001: Create documentation for API endpoints

Created: 2025-04-10
Status: Action [ ]
Tags: #task/mcp

## Task Description

Create comprehensive documentation for the MCP server API endpoints.

## Progress Log

### 2025-04-10 14:30
- Task created by LLM
- Initial research on existing API endpoints

## Related Files

- [[BeWhyOrg/Local/AI/MCP Actions/API Documentation]]
```

## Task Update Process

When an LLM updates a task:

1. It finds the task in the daily note by its ID
2. It updates the task status according to the flow
3. It updates the log file with the latest progress
4. It links any new or updated files

Example updated task:
```markdown
- [B] ⏫ MCP-001 Create documentation for API endpoints #task/mcp 📅 2025-04-10 ⏳ 2025-04-15
```

Example updated log file:
```markdown
# MCP-001: Create documentation for API endpoints

Created: 2025-04-10
Status: Planeamento [B]
Tags: #task/mcp

## Task Description

Create comprehensive documentation for the MCP server API endpoints.

## Progress Log

### 2025-04-10 14:30
- Task created by LLM
- Initial research on existing API endpoints

### 2025-04-10 15:45
- Identified all API endpoints
- Created outline for documentation
- Status updated to Planeamento [B]

## Related Files

- [[BeWhyOrg/Local/AI/MCP Actions/API Documentation]]
```

## Task Completion

When a task is ready for human review:

1. The LLM updates the task status to Testes [?]
2. The LLM updates the log file with the final progress
3. The LLM notifies the human that the task is ready for review

After review, the human can:
1. Mark the task as Terminado [-] if it's complete but needs further review
2. Mark the task as Done [x] if it's fully complete
3. Provide feedback and reset the status if changes are needed

## Task Queries

You can use the Tasks plugin to query tasks:


````markdown
```tasks
not done
tags include task/mcp
sort by priority
```

MCP API Integration

The MCP server provides API endpoints for task management:

- POST /api/obsidian-mcp-actions/task/create: Create a new task
    
- POST /api/obsidian-mcp-actions/task/update: Update an existing task
    
- GET /api/obsidian-mcp-actions/task/get: Get information about a task
    

See the [[`BeWhyOrg/Local/AI/MCP Actions/API Documentation]] for details on these endpoints.

```