# API Documentation

This document provides detailed information about the API endpoints available in the Obsidian MCP Actions system.

## For LLMs

If you are an LLM interacting with this system, please follow these guidelines:

1. **Task Creation**: When asked to perform a task, create a task in the daily note and a log file
2. **Status Updates**: Only update task status up to Testes [?] - never mark as Terminado [-] or Done [x]
3. **Documentation**: Create or update documentation in the appropriate locations
4. **Linking**: Always link related files using Obsidian's [[file]] syntax
5. **Logging**: Keep detailed logs of your actions in the task log file

Remember that your role is to assist with documentation, research, and implementation planning, but final approval and completion should be done by a human.

## Base URL

All API endpoints are relative to the MCP server base URL:

```
http://localhost:3000/api/obsidian-mcp-actions
```

## Authentication

All API requests require authentication using the API key specified in the MCP server configuration.

Include the API key in the `Authorization` header:

```
Authorization: Bearer your-api-key-here
```

## Task Management Endpoints

### Create Task

Creates a new task in the daily note and a corresponding log file.

**Endpoint**: `POST /task/create`

**Request Body**:
```json
{
  "description": "Create documentation for API endpoints",
  "priority": "high",
  "area": "mcp",
  "schedule_date": "2025-04-10",
  "due_date": "2025-04-15",
  "details": "Create comprehensive documentation for the MCP server API endpoints."
}
```

**Priority Options**:
- `high`: ⏫
- `medium`: 🔼
- `normal`: (no symbol)
- `low`: ⏬

**Response**:
```json
{
  "success": true,
  "task_id": "MCP-001",
  "task_file": "vault/Logs/Tasks/MCP-001-Create-documentation-for-API-endpoints.md",
  "daily_note": "vault/Logs/Daily Logs/2025-04-10.md"
}
```

### Update Task

Updates an existing task's status and log file.

**Endpoint**: `POST /task/update`

**Request Body**:
```json
{
  "task_id": "MCP-001",
  "status": "planning",
  "progress": "Identified all API endpoints\nCreated outline for documentation",
  "related_files": [
    "BeWhyOrg/Local/AI/MCP Actions/API Documentation"
  ]
}
```

**Status Options**:
- `action`: Action [ ]
- `planning`: Planeamento [B]
- `in_progress`: In Progress [d]
- `testing`: Testes [?]

**Response**:
```json
{
  "success": true,
  "task_id": "MCP-001",
  "new_status": "planning",
  "task_file": "vault/Logs/Tasks/MCP-001-Create-documentation-for-API-endpoints.md"
}
```

### Get Task

Retrieves information about a task.

**Endpoint**: `GET /task/get`

**Query Parameters**:
- `task_id`: The ID of the task to retrieve

**Example**: `GET /task/get?task_id=MCP-001`

**Response**:
```json
{
  "success": true,
  "task_id": "MCP-001",
  "description": "Create documentation for API endpoints",
  "status": "planning",
  "priority": "high",
  "area": "mcp",
  "schedule_date": "2025-04-10",
  "due_date": "2025-04-15",
  "task_file": "vault/Logs/Tasks/MCP-001-Create-documentation-for-API-endpoints.md",
  "daily_note": "vault/Logs/Daily Logs/2025-04-10.md",
  "related_files": [
    "BeWhyOrg/Local/AI/MCP Actions/API Documentation"
  ]
}
```

## Documentation Management Endpoints

### Create Document

Creates a new document in the vault.

**Endpoint**: `POST /document/create`

**Request Body**:
```json
{
  "path": "BeWhyOrg/Local/AI/MCP Actions/New Document.md",
  "content": "# New Document\n\nThis is a new document created by the MCP server.",
  "task_id": "MCP-001"
}
```

**Response**:
```json
{
  "success": true,
  "file_path": "vault/BeWhyOrg/Local/AI/MCP Actions/New Document.md",
  "task_id": "MCP-001"
}
```

### Update Document

Updates an existing document in the vault.

**Endpoint**: `POST /document/update`

**Request Body**:
```json
{
  "path": "BeWhyOrg/Local/AI/MCP Actions/New Document.md",
  "content": "# Updated Document\n\nThis document has been updated by the MCP server.",
  "task_id": "MCP-001"
}
```

**Response**:
```json
{
  "success": true,
  "file_path": "vault/BeWhyOrg/Local/AI/MCP Actions/New Document.md",
  "task_id": "MCP-001"
}
```

### Get Document

Retrieves the content of a document.

**Endpoint**: `GET /document/get`

**Query Parameters**:
- `path`: The path of the document to retrieve

**Example**: `GET /document/get?path=BeWhyOrg/Local/AI/MCP Actions/New Document.md`

**Response**:
```json
{
  "success": true,
  "file_path": "vault/BeWhyOrg/Local/AI/MCP Actions/New Document.md",
  "content": "# Updated Document\n\nThis document has been updated by the MCP server."
}
```

## Search Endpoints

### Search Vault

Searches the vault for documents matching a query.

**Endpoint**: `GET /search`

**Query Parameters**:
- `query`: The search query
- `limit`: (Optional) The maximum number of results to return (default: 10)

**Example**: `GET /search?query=MCP&limit=5`

**Response**:
```json
{
  "success": true,
  "results": [
    {
      "file_path": "vault/BeWhyOrg/Local/AI/MCP Actions/API Documentation.md",
      "score": 0.95
    },
    {
      "file_path": "vault/BeWhyOrg/Local/AI/MCP Actions/README.md",
      "score": 0.85
    },
    {
      "file_path": "vault/BeWhyOrg/Local/AI/MCPs/List/obsidian-mcp-server.md",
      "score": 0.75
    }
  ]
}
```

## Error Handling

All API endpoints return a standard error format:

```json
{
  "success": false,
  "error": "Error message",
  "code": "ERROR_CODE"
}
```

Common error codes:
- `AUTHENTICATION_ERROR`: Invalid or missing API key
- `NOT_FOUND`: Requested resource not found
- `VALIDATION_ERROR`: Invalid request parameters
- `INTERNAL_ERROR`: Internal server error
