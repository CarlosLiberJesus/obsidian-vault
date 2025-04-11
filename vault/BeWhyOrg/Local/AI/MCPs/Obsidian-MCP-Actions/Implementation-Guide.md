# Implementation Guide

This document provides guidance on implementing the Obsidian MCP Actions system in the MCP server.

## Prerequisites

- Node.js and npm installed
- Obsidian with the Local REST API plugin enabled
- MCP server installed and configured

## Implementation Steps

### 1. Add API Endpoints to MCP Server

Create a new file in the MCP server project:

```javascript
// src/routes/obsidian-mcp-actions.js

const express = require('express');
const router = express.Router();
const obsidianApi = require('../services/obsidian-api');
const { authenticateApiKey } = require('../middleware/auth');

// Apply authentication middleware to all routes
router.use(authenticateApiKey);

// Task Management Endpoints

// Create a new task
router.post('/task/create', async (req, res) => {
  try {
    const { description, priority, area, schedule_date, due_date, details } = req.body;
    
    // Generate a unique task ID
    const taskCount = await obsidianApi.getTaskCount();
    const taskId = `MCP-${(taskCount + 1).toString().padStart(3, '0')}`;
    
    // Format the task for the daily note
    const prioritySymbol = getPrioritySymbol(priority);
    const taskLine = `- [ ] ${prioritySymbol} ${taskId} ${description} #task/${area} 📅 ${schedule_date} ⏳ ${due_date}`;
    
    // Add the task to the daily note
    const today = new Date();
    const dailyNotePath = `vault/Logs/Daily-Logs/${today.getFullYear()}-${(today.getMonth() + 1).toString().padStart(2, '0')}-${today.getDate().toString().padStart(2, '0')}.md`;
    await obsidianApi.addTaskToDailyNote(dailyNotePath, taskLine);
    
    // Create the task log file
    const taskFileName = `${taskId}-${description.replace(/\s+/g, '-')}.md`;
    const taskFilePath = `vault/Logs/Tasks/${taskFileName}`;
    const taskFileContent = createTaskLogContent(taskId, description, details, area);
    await obsidianApi.createFile(taskFilePath, taskFileContent);
    
    res.json({
      success: true,
      task_id: taskId,
      task_file: taskFilePath,
      daily_note: dailyNotePath
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Update a task's status
router.post('/task/update', async (req, res) => {
  try {
    const { task_id, status, progress, related_files } = req.body;
    
    // Update the task in the daily note
    const statusSymbol = getStatusSymbol(status);
    await obsidianApi.updateTaskStatus(task_id, statusSymbol);
    
    // Update the task log file
    const taskFiles = await obsidianApi.findTaskLogFile(task_id);
    if (taskFiles.length === 0) {
      throw new Error(`Task log file for ${task_id} not found`);
    }
    
    const taskFilePath = taskFiles[0];
    const now = new Date();
    const timestamp = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')} ${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}`;
    
    const progressUpdate = `### ${timestamp}\n${progress.split('\n').map(line => `- ${line}`).join('\n')}\n- Status updated to ${getStatusName(status)} [${statusSymbol}]`;
    
    await obsidianApi.updateTaskLogFile(taskFilePath, progressUpdate, status, related_files);
    
    res.json({
      success: true,
      task_id,
      new_status: status,
      task_file: taskFilePath
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Get task information
router.get('/task/get', async (req, res) => {
  try {
    const { task_id } = req.query;
    
    // Find the task in daily notes
    const taskInfo = await obsidianApi.getTaskInfo(task_id);
    
    // Find the task log file
    const taskFiles = await obsidianApi.findTaskLogFile(task_id);
    if (taskFiles.length === 0) {
      throw new Error(`Task log file for ${task_id} not found`);
    }
    
    const taskFilePath = taskFiles[0];
    const taskFileContent = await obsidianApi.getFileContent(taskFilePath);
    
    res.json({
      success: true,
      ...taskInfo,
      task_file: taskFilePath
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Document Management Endpoints

// Create a new document
router.post('/document/create', async (req, res) => {
  try {
    const { path, content, task_id } = req.body;
    
    // Create the document
    const filePath = `vault/${path}`;
    await obsidianApi.createFile(filePath, content);
    
    // Update the task log file if task_id is provided
    if (task_id) {
      const taskFiles = await obsidianApi.findTaskLogFile(task_id);
      if (taskFiles.length > 0) {
        const taskFilePath = taskFiles[0];
        await obsidianApi.addRelatedFileToTaskLog(taskFilePath, path);
      }
    }
    
    res.json({
      success: true,
      file_path: filePath,
      task_id
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Update an existing document
router.post('/document/update', async (req, res) => {
  try {
    const { path, content, task_id } = req.body;
    
    // Update the document
    const filePath = `vault/${path}`;
    await obsidianApi.updateFile(filePath, content);
    
    // Update the task log file if task_id is provided
    if (task_id) {
      const taskFiles = await obsidianApi.findTaskLogFile(task_id);
      if (taskFiles.length > 0) {
        const taskFilePath = taskFiles[0];
        await obsidianApi.addRelatedFileToTaskLog(taskFilePath, path);
      }
    }
    
    res.json({
      success: true,
      file_path: filePath,
      task_id
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Get document content
router.get('/document/get', async (req, res) => {
  try {
    const { path } = req.query;
    
    // Get the document content
    const filePath = `vault/${path}`;
    const content = await obsidianApi.getFileContent(filePath);
    
    res.json({
      success: true,
      file_path: filePath,
      content
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Search endpoint
router.get('/search', async (req, res) => {
  try {
    const { query, limit = 10 } = req.query;
    
    // Search the vault
    const results = await obsidianApi.searchVault(query, limit);
    
    res.json({
      success: true,
      results
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

// Helper functions

function getPrioritySymbol(priority) {
  switch (priority) {
    case 'high': return '⏫';
    case 'medium': return '🔼';
    case 'low': return '⏬';
    default: return '';
  }
}

function getStatusSymbol(status) {
  switch (status) {
    case 'action': return ' ';
    case 'planning': return 'B';
    case 'in_progress': return 'd';
    case 'testing': return '?';
    default: return ' ';
  }
}

function getStatusName(status) {
  switch (status) {
    case 'action': return 'Action';
    case 'planning': return 'Planeamento';
    case 'in_progress': return 'In Progress';
    case 'testing': return 'Testes';
    default: return 'Action';
  }
}

function createTaskLogContent(taskId, description, details, area) {
  const today = new Date();
  const dateStr = `${today.getFullYear()}-${(today.getMonth() + 1).toString().padStart(2, '0')}-${today.getDate().toString().padStart(2, '0')}`;
  const timeStr = `${today.getHours().toString().padStart(2, '0')}:${today.getMinutes().toString().padStart(2, '0')}`;
  
  return `# ${taskId}: ${description}

Created: ${dateStr}
Status: Action [ ]
Tags: #task/${area}

## Task Description

${details}

## Progress Log

### ${dateStr} ${timeStr}
- Task created by LLM
- Initial setup and planning

## Related Files

`;
}

module.exports = router;
```

### 2. Implement Obsidian API Service

Create a service to interact with the Obsidian Local REST API:

```javascript
// src/services/obsidian-api.js

const axios = require('axios');
const fs = require('fs').promises;
const path = require('path');

// Configure Obsidian API
const obsidianApi = axios.create({
  baseURL: process.env.OBSIDIAN_PROTOCOL + '://' + process.env.OBSIDIAN_HOST + ':' + process.env.OBSIDIAN_PORT,
  headers: {
    'Authorization': 'Bearer ' + process.env.OBSIDIAN_API_KEY
  },
  httpsAgent: process.env.VERIFY_SSL === 'false' ? new (require('https').Agent)({ rejectUnauthorized: false }) : undefined
});

// Get the content of a file
async function getFileContent(filePath) {
  try {
    const response = await obsidianApi.get('/vault/' + filePath);
    return response.data;
  } catch (error) {
    throw new Error(`Failed to get file content: ${error.message}`);
  }
}

// Create a new file
async function createFile(filePath, content) {
  try {
    const response = await obsidianApi.put('/vault/' + filePath, content);
    return response.data;
  } catch (error) {
    throw new Error(`Failed to create file: ${error.message}`);
  }
}

// Update an existing file
async function updateFile(filePath, content) {
  try {
    const response = await obsidianApi.put('/vault/' + filePath, content);
    return response.data;
  } catch (error) {
    throw new Error(`Failed to update file: ${error.message}`);
  }
}

// Add a task to the daily note
async function addTaskToDailyNote(dailyNotePath, taskLine) {
  try {
    // Get the current content of the daily note
    let content = '';
    try {
      content = await getFileContent(dailyNotePath);
    } catch (error) {
      // If the file doesn't exist, create it with a basic template
      content = createDailyNoteTemplate(dailyNotePath);
      await createFile(dailyNotePath, content);
    }
    
    // Find the Quick Add section
    const quickAddIndex = content.indexOf('## Tarefas QuickAdd');
    if (quickAddIndex === -1) {
      throw new Error('Quick Add section not found in daily note');
    }
    
    // Find the next section after Quick Add
    let nextSectionIndex = content.indexOf('##', quickAddIndex + 1);
    if (nextSectionIndex === -1) {
      nextSectionIndex = content.length;
    }
    
    // Insert the task at the beginning of the Quick Add section
    const beforeQuickAdd = content.substring(0, quickAddIndex + 18); // +18 to include the section title
    const afterQuickAdd = content.substring(quickAddIndex + 18, nextSectionIndex);
    const afterNextSection = content.substring(nextSectionIndex);
    
    const newContent = beforeQuickAdd + '\n\n' + taskLine + '\n' + afterQuickAdd + afterNextSection;
    
    // Update the daily note
    await updateFile(dailyNotePath, newContent);
    
    return true;
  } catch (error) {
    throw new Error(`Failed to add task to daily note: ${error.message}`);
  }
}

// Update a task's status in the daily note
async function updateTaskStatus(taskId, statusSymbol) {
  try {
    // Find the daily note containing the task
    const dailyNotes = await findDailyNotesWithTask(taskId);
    if (dailyNotes.length === 0) {
      throw new Error(`Task ${taskId} not found in any daily note`);
    }
    
    const dailyNotePath = dailyNotes[0];
    const content = await getFileContent(dailyNotePath);
    
    // Find the task line
    const taskRegex = new RegExp(`- \\[.\\] .* ${taskId} .*`, 'g');
    const match = taskRegex.exec(content);
    if (!match) {
      throw new Error(`Task ${taskId} not found in daily note ${dailyNotePath}`);
    }
    
    // Update the task status
    const taskLine = match[0];
    const updatedTaskLine = taskLine.replace(/- \[.\]/, `- [${statusSymbol}]`);
    
    // Update the daily note
    const newContent = content.replace(taskLine, updatedTaskLine);
    await updateFile(dailyNotePath, newContent);
    
    return true;
  } catch (error) {
    throw new Error(`Failed to update task status: ${error.message}`);
  }
}

// Find daily notes containing a specific task
async function findDailyNotesWithTask(taskId) {
  try {
    // Get all daily notes
    const dailyNotes = await obsidianApi.get('/search', {
      params: {
        query: 'path:Logs/Daily-Logs'
      }
    });
    
    const matchingNotes = [];
    
    // Check each daily note for the task
    for (const note of dailyNotes.data) {
      const content = await getFileContent(note.path);
      if (content.includes(taskId)) {
        matchingNotes.push(note.path);
      }
    }
    
    return matchingNotes;
  } catch (error) {
    throw new Error(`Failed to find daily notes with task: ${error.message}`);
  }
}

// Find the task log file for a specific task
async function findTaskLogFile(taskId) {
  try {
    // Search for task log files
    const taskLogs = await obsidianApi.get('/search', {
      params: {
        query: `path:Logs/Tasks ${taskId}`
      }
    });
    
    return taskLogs.data.map(log => log.path);
  } catch (error) {
    throw new Error(`Failed to find task log file: ${error.message}`);
  }
}

// Update the task log file
async function updateTaskLogFile(taskFilePath, progressUpdate, status, relatedFiles) {
  try {
    // Get the current content of the task log file
    const content = await getFileContent(taskFilePath);
    
    // Update the status
    const statusRegex = /Status: .*/;
    const statusMatch = statusRegex.exec(content);
    if (!statusMatch) {
      throw new Error(`Status line not found in task log file ${taskFilePath}`);
    }
    
    const statusLine = statusMatch[0];
    const statusName = getStatusName(status);
    const statusSymbol = getStatusSymbol(status);
    const updatedStatusLine = `Status: ${statusName} [${statusSymbol}]`;
    
    // Add the progress update
    const progressLogIndex = content.indexOf('## Progress Log');
    if (progressLogIndex === -1) {
      throw new Error(`Progress Log section not found in task log file ${taskFilePath}`);
    }
    
    const beforeProgressLog = content.substring(0, progressLogIndex + 14); // +14 to include the section title
    const afterProgressLog = content.substring(progressLogIndex + 14);
    
    // Add related files if provided
    let relatedFilesContent = '';
    if (relatedFiles && relatedFiles.length > 0) {
      const relatedFilesIndex = content.indexOf('## Related Files');
      if (relatedFilesIndex !== -1) {
        const beforeRelatedFiles = content.substring(0, relatedFilesIndex + 16); // +16 to include the section title
        let afterRelatedFiles = content.substring(relatedFilesIndex + 16);
        
        // Add each related file if it's not already there
        for (const file of relatedFiles) {
          if (!afterRelatedFiles.includes(`[[${file}]]`)) {
            afterRelatedFiles += `\n- [[${file}]]`;
          }
        }
        
        relatedFilesContent = beforeRelatedFiles + afterRelatedFiles;
      }
    }
    
    // Combine everything
    let newContent = content.replace(statusLine, updatedStatusLine);
    newContent = newContent.replace(beforeProgressLog + afterProgressLog, beforeProgressLog + '\n\n' + progressUpdate + '\n' + afterProgressLog);
    
    if (relatedFilesContent) {
      newContent = relatedFilesContent;
    }
    
    // Update the task log file
    await updateFile(taskFilePath, newContent);
    
    return true;
  } catch (error) {
    throw new Error(`Failed to update task log file: ${error.message}`);
  }
}

// Add a related file to the task log
async function addRelatedFileToTaskLog(taskFilePath, filePath) {
  try {
    // Get the current content of the task log file
    const content = await getFileContent(taskFilePath);
    
    // Find the Related Files section
    const relatedFilesIndex = content.indexOf('## Related Files');
    if (relatedFilesIndex === -1) {
      throw new Error(`Related Files section not found in task log file ${taskFilePath}`);
    }
    
    // Check if the file is already listed
    if (content.includes(`[[${filePath}]]`)) {
      return true;
    }
    
    // Add the file to the Related Files section
    const beforeRelatedFiles = content.substring(0, relatedFilesIndex + 16); // +16 to include the section title
    const afterRelatedFiles = content.substring(relatedFilesIndex + 16);
    
    const newContent = beforeRelatedFiles + '\n\n- [[' + filePath + ']]' + afterRelatedFiles;
    
    // Update the task log file
    await updateFile(taskFilePath, newContent);
    
    return true;
  } catch (error) {
    throw new Error(`Failed to add related file to task log: ${error.message}`);
  }
}

// Get information about a task
async function getTaskInfo(taskId) {
  try {
    // Find the daily note containing the task
    const dailyNotes = await findDailyNotesWithTask(taskId);
    if (dailyNotes.length === 0) {
      throw new Error(`Task ${taskId} not found in any daily note`);
    }
    
    const dailyNotePath = dailyNotes[0];
    const content = await getFileContent(dailyNotePath);
    
    // Find the task line
    const taskRegex = new RegExp(`- \\[(.?)\\] (.*?) ${taskId} (.*?) #task/(.*?)( 📅 (.*?))?( ⏳ (.*?))?($|\\s)`, 'g');
    const match = taskRegex.exec(content);
    if (!match) {
      throw new Error(`Task ${taskId} not found in daily note ${dailyNotePath}`);
    }
    
    // Parse the task information
    const status = getStatusFromSymbol(match[1]);
    const priority = getPriorityFromSymbol(match[2]);
    const description = match[3].trim();
    const area = match[4].trim();
    const scheduleDate = match[6] || '';
    const dueDate = match[8] || '';
    
    // Find related files
    const taskFiles = await findTaskLogFile(taskId);
    let relatedFiles = [];
    
    if (taskFiles.length > 0) {
      const taskFileContent = await getFileContent(taskFiles[0]);
      const relatedFilesRegex = /\[\[(.*?)\]\]/g;
      let fileMatch;
      while ((fileMatch = relatedFilesRegex.exec(taskFileContent)) !== null) {
        relatedFiles.push(fileMatch[1]);
      }
    }
    
    return {
      task_id: taskId,
      description,
      status,
      priority,
      area,
      schedule_date: scheduleDate,
      due_date: dueDate,
      daily_note: dailyNotePath,
      related_files: relatedFiles
    };
  } catch (error) {
    throw new Error(`Failed to get task information: ${error.message}`);
  }
}

// Get the total number of tasks
async function getTaskCount() {
  try {
    // Search for task log files
    const taskLogs = await obsidianApi.get('/search', {
      params: {
        query: 'path:Logs/Tasks'
      }
    });
    
    return taskLogs.data.length;
  } catch (error) {
    throw new Error(`Failed to get task count: ${error.message}`);
  }
}

// Search the vault
async function searchVault(query, limit) {
  try {
    const response = await obsidianApi.get('/search', {
      params: {
        query,
        limit
      }
    });
    
    return response.data.map(result => ({
      file_path: result.path,
      score: result.score
    }));
  } catch (error) {
    throw new Error(`Failed to search vault: ${error.message}`);
  }
}

// Helper functions

function getStatusFromSymbol(symbol) {
  switch (symbol) {
    case ' ': return 'action';
    case 'B': return 'planning';
    case 'd': return 'in_progress';
    case '?': return 'testing';
    case '-': return 'completed';
    case 'x': return 'done';
    default: return 'action';
  }
}

function getPriorityFromSymbol(symbol) {
  if (symbol.includes('⏫')) return 'high';
  if (symbol.includes('🔼')) return 'medium';
  if (symbol.includes('⏬')) return 'low';
  return 'normal';
}

function getStatusSymbol(status) {
  switch (status) {
    case 'action': return ' ';
    case 'planning': return 'B';
    case 'in_progress': return 'd';
    case 'testing': return '?';
    case 'completed': return '-';
    case 'done': return 'x';
    default: return ' ';
  }
}

function getStatusName(status) {
  switch (status) {
    case 'action': return 'Action';
    case 'planning': return 'Planeamento';
    case 'in_progress': return 'In Progress';
    case 'testing': return 'Testes';
    case 'completed': return 'Terminado';
    case 'done': return 'Done';
    default: return 'Action';
  }
}

function createDailyNoteTemplate(dailyNotePath) {
  const filename = path.basename(dailyNotePath, '.md');
  const date = new Date(filename);
  const dayOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][date.getDay()];
  
  const yesterday = new Date(date);
  yesterday.setDate(date.getDate() - 1);
  const yesterdayStr = `${yesterday.getFullYear()}-${(yesterday.getMonth() + 1).toString().padStart(2, '0')}-${yesterday.getDate().toString().padStart(2, '0')}`;
  
  const tomorrow = new Date(date);
  tomorrow.setDate(date.getDate() + 1);
  const tomorrowStr = `${tomorrow.getFullYear()}-${(tomorrow.getMonth() + 1).toString().padStart(2, '0')}-${tomorrow.getDate().toString().padStart(2, '0')}`;
  
  const weekNumber = getWeekNumber(date);
  
  return `# ${dayOfWeek}, ${date.getDate()} de ${['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'][date.getMonth()]} de ${date.getFullYear()}
[[Daily-Logs/${yesterdayStr}|Ontem]]  <-> [[Daily-Logs/${tomorrowStr}|Amanhã]]
Visão Semanal: [[Weekly-Logs/${date.getFullYear()}-W${weekNumber}| Semana ${weekNumber}]]


> [!atraso]
> \`\`\`tasks
> not done
> due before ${filename}
> sort by priority
> \`\`\`

> [!tarefas]
>\`\`\`tasks
>not done
>(due on ${filename}) OR ((scheduled in or before ${filename}) AND (due in or after ${filename}))
>hide due date
>sort by priority
>\`\`\`

> [!summary]
> \`\`\`tasks
> done on ${filename}
> \`\`\`


## Objectivos



## Notas



## Tarefas QuickAdd



> [!amanha]
> 
> ## 💼 Tarefas
>
>\`\`\`tasks
>not done
>(due on ${tomorrowStr}) OR ((scheduled in or before ${tomorrowStr}) AND (due in or after ${tomorrowStr}))
>hide due date
>sort by priority
>\`\`\`

`;
}

function getWeekNumber(date) {
  const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()));
  const dayNum = d.getUTCDay() || 7;
  d.setUTCDate(d.getUTCDate() + 4 - dayNum);
  const yearStart = new Date(Date.UTC(d.getUTCFullYear(), 0, 1));
  return Math.ceil((((d - yearStart) / 86400000) + 1) / 7);
}

module.exports = {
  getFileContent,
  createFile,
  updateFile,
  addTaskToDailyNote,
  updateTaskStatus,
  findDailyNotesWithTask,
  findTaskLogFile,
  updateTaskLogFile,
  addRelatedFileToTaskLog,
  getTaskInfo,
  getTaskCount,
  searchVault
};
```

### 3. Register the Routes in the MCP Server

Add the routes to the main app:

```javascript
// src/index.js

const express = require('express');
const app = express();
const obsidianMcpActions = require('./routes/obsidian-mcp-actions');

// ... other imports and middleware

// Register routes
app.use('/api/obsidian-mcp-actions', obsidianMcpActions);

// ... other routes and server setup
```

### 4. Update Environment Variables

Add the necessary environment variables to the `.env` file:

```
OBSIDIAN_API_KEY=your_api_key_here
VERIFY_SSL=false
OBSIDIAN_PROTOCOL=https
OBSIDIAN_HOST=127.0.0.1
OBSIDIAN_PORT=27124
```

## Testing the Implementation

### 1. Start the MCP Server

```bash
cd ~/IDEs/obsidian-mcp-server
npm start
```

### 2. Create a Test Task

```bash
curl -X POST http://localhost:3000/api/obsidian-mcp-actions/task/create \
  -H "Authorization: Bearer your-api-key-here" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "Test the Obsidian MCP Actions system",
    "priority": "high",
    "area": "mcp",
    "schedule_date": "2025-04-11",
    "due_date": "2025-04-15",
    "details": "Create a test task to verify that the Obsidian MCP Actions system is working correctly."
  }'
```

### 3. Update the Task Status

```bash
curl -X POST http://localhost:3000/api/obsidian-mcp-actions/task/update \
  -H "Authorization: Bearer your-api-key-here" \
  -H "Content-Type: application/json" \
  -d '{
    "task_id": "MCP-001",
    "status": "planning",
    "progress": "Created test task\nVerified that it appears in the daily note",
    "related_files": [
      "BeWhyOrg/Local/AI/MCPs/Obsidian-MCP-Actions/Examples/Example-Task"
    ]
  }'
```

### 4. Get Task Information

```bash
curl -X GET "http://localhost:3000/api/obsidian-mcp-actions/task/get?task_id=MCP-001" \
  -H "Authorization: Bearer your-api-key-here"
```

## Next Steps

After implementing the basic functionality, consider these enhancements:

1. **Error Handling**: Improve error handling and validation
2. **Logging**: Add detailed logging for debugging
3. **Authentication**: Enhance authentication for better security
4. **UI Integration**: Create a simple UI for managing tasks
5. **Webhooks**: Add webhook support for notifications
6. **Testing**: Write automated tests for the API endpoints
