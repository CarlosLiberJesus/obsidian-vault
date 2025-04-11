# Example Task: MCP-001

This document demonstrates how a task would be created and managed using the Obsidian MCP Actions system.

## Task in Daily Note

The following task would be added to the daily note under the ## Quick Add section:

```markdown
- [ ] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15
```

## Task Log File

A corresponding log file would be created at `vault/Logs/Tasks/MCP-001-Create-API-documentation-for-Obsidian-MCP-Actions.md`:

```markdown
# MCP-001: Create API documentation for Obsidian MCP Actions

Created: 2025-04-11
Status: Action [ ]
Tags: #task/mcp

## Task Description

Create comprehensive API documentation for the Obsidian MCP Actions system, including all endpoints, request/response formats, and examples.

## Progress Log

### 2025-04-11 09:30
- Task created by LLM
- Initial research on existing API endpoints
- Identified key endpoints to document

## Related Files

- [[BeWhyOrg/Local/AI/MCPs/Obsidian-MCP-Actions/API-Documentation]]
```

## Task Status Updates

As the LLM works on the task, it would update the status in both the daily note and the log file:

### Planning Phase

Daily note:
```markdown
- [B] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15
```

Log file update:
```markdown
### 2025-04-11 10:15
- Created outline for API documentation
- Researched standard API documentation formats
- Status updated to Planeamento [B]
```

### Implementation Phase

Daily note:
```markdown
- [d] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15
```

Log file update:
```markdown
### 2025-04-11 11:30
- Drafted documentation for task management endpoints
- Added request/response examples
- Status updated to In Progress [d]
```

### Testing Phase

Daily note:
```markdown
- [?] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15
```

Log file update:
```markdown
### 2025-04-11 14:45
- Completed documentation for all endpoints
- Verified examples and formats
- Ready for human review
- Status updated to Testes [?]
```

## Human Review

After the LLM has completed the task, a human would review it and update the status:

Daily note:
```markdown
- [-] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15
```

Log file update:
```markdown
### 2025-04-11 16:30
- Human review completed
- Minor formatting issues fixed
- Status updated to Terminado [-]
```

## Final Completion

Once fully satisfied, the human would mark the task as done:

Daily note:
```markdown
- [x] ⏫ MCP-001 Create API documentation for Obsidian MCP Actions #task/mcp 📅 2025-04-11 ⏳ 2025-04-15 ✅ 2025-04-11
```

Log file update:
```markdown
### 2025-04-11 17:00
- Task fully completed and approved
- Documentation published
- Status updated to Done [x]
```

## API Calls

Here's how this task would be created using the API:

```bash
curl -X POST http://localhost:3000/api/obsidian-mcp-actions/task/create \
  -H "Authorization: Bearer your-api-key-here" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "Create API documentation for Obsidian MCP Actions",
    "priority": "high",
    "area": "mcp",
    "schedule_date": "2025-04-11",
    "due_date": "2025-04-15",
    "details": "Create comprehensive API documentation for the Obsidian MCP Actions system, including all endpoints, request/response formats, and examples."
  }'
```

And here's how the status would be updated:

```bash
curl -X POST http://localhost:3000/api/obsidian-mcp-actions/task/update \
  -H "Authorization: Bearer your-api-key-here" \
  -H "Content-Type: application/json" \
  -d '{
    "task_id": "MCP-001",
    "status": "planning",
    "progress": "Created outline for API documentation\nResearched standard API documentation formats",
    "related_files": [
      "BeWhyOrg/Local/AI/MCPs/Obsidian-MCP-Actions/API-Documentation"
    ]
  }'
```
