# Task Logs

This folder contains detailed logs for tasks created through the Obsidian MCP Actions system.

## Purpose

Task logs serve as a comprehensive record of:
- Task details and requirements
- Progress updates and status changes
- Implementation details and decisions
- Related files and documentation

## Naming Convention

Task log files follow this naming convention:

```
MCP-XXX-Brief-Description.md
```

Where:
- `MCP-XXX` is the unique task ID (e.g., MCP-001)
- `Brief-Description` is a short description of the task with hyphens instead of spaces

For example:
```
MCP-001-Create-API-documentation-for-Obsidian-MCP-Actions.md
```

## File Structure

Each task log file has the following structure:

```markdown
# MCP-XXX: Brief Description

Created: YYYY-MM-DD
Status: Current Status [Symbol]
Tags: #task/area

## Task Description

Detailed description of the task.

## Progress Log

### YYYY-MM-DD HH:MM
- Progress update 1
- Progress update 2
- Status updated to New Status [Symbol]

### YYYY-MM-DD HH:MM
- Progress update 3
- Progress update 4
- Status updated to New Status [Symbol]

## Implementation Details

Details about the implementation, including code snippets, decisions, and challenges.

## Related Files

- [[Path/To/Related/File1]]
- [[Path/To/Related/File2]]

## Notes

Additional notes or information about the task.
```

## Task Status Flow

Tasks progress through the following statuses:

1. **Action [ ]**: Initial status when a task is created
2. **Planeamento [B]**: Planning phase, when the task is being planned
3. **In Progress [d]**: Implementation phase, when the task is being worked on
4. **Testes [?]**: Testing phase, when the task is being tested
5. **Terminado [-]**: Completed phase, when the task is finished but not yet reviewed
6. **Done [x]**: Final status when a task is completed and reviewed

LLMs will only update tasks to statuses 1-4. Only humans should mark tasks as Terminado [-] or Done [x].

## Example

See [MCP-001-Create-API-documentation-for-Obsidian-MCP-Actions.md](MCP-001-Create-API-documentation-for-Obsidian-MCP-Actions.md) for an example of a task log.
