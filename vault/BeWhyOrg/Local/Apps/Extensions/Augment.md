# Augment Extension

## Overview

Augment is an AI coding assistant extension that helps with understanding and modifying codebases. It's powered by Claude 3.7 Sonnet and provides advanced capabilities for working with code.

## Key Features

- **Codebase Understanding**: Quickly understands complex codebases
- **Code Generation**: Helps write new code based on requirements
- **Code Modification**: Assists with modifying existing code
- **Explanation**: Explains how code works and why it's structured a certain way
- **MCP Integration**: Can integrate with Master Control Programs (MCPs) like the Obsidian MCP server

## Configuration for MCP Integration

### Method 1

1. Open VSCode Settings (Ctrl+Shift+P)
2. Look for Preference: User Preferences (JSON)
3. test it by asking about tasks....

```json
"augment.advanced": {
	"mcpServers": [
		{
			"name": "obsidian-mcp-server",
			"command": "node",
			"args": ["/home/carlos/MCPs/obsidian-mcp-server/build/index.js"],
			"env": {
				"OBSIDIAN_API_KEY": "your_api_key_here",
				"VERIFY_SSL": "false",
				"OBSIDIAN_PROTOCOL": "https",
				"OBSIDIAN_HOST": "127.0.0.1",
				"OBSIDIAN_PORT": "27124",
				"REQUEST_TIMEOUT": "5000",
				"MAX_CONTENT_LENGTH": "52428800",
				"MAX_BODY_LENGTH": "52428800"
			}
		}
	]
}
```

### Method 2
To configure Augment to work with the Obsidian MCP server:

1. Open VSCode Settings (Ctrl+,)
2. Search for "Augment"
3. Look for the "MCP Servers" setting
4. Add the following configuration:

```json
{
  "mcpServers": {
    "obsidian-mcp-server": {
      "command": "node",
      "args": ["/home/carlos/MCPs/obsidian-mcp-server/build/index.js"],
      "env": {
        "OBSIDIAN_API_KEY": "your_api_key_here",
        "VERIFY_SSL": "false",
        "OBSIDIAN_PROTOCOL": "https",
        "OBSIDIAN_HOST": "127.0.0.1",
        "OBSIDIAN_PORT": "27124"
      }
    }
  },
  "augment.mcpServer": "obsidian-mcp-server"
}
```

Replace `/path/to/obsidian-mcp-server` with the actual path to your obsidian-mcp-server installation, and `your_api_key_here` with the API key from the Obsidian Local REST API plugin.

## Using Augment with Obsidian MCP Actions

Once configured, Augment can interact with your Obsidian vault through the MCP server. Here's how to use it:

1. **Creating Tasks**: Augment can create tasks in your daily notes and corresponding log files
2. **Updating Documentation**: Augment can create or update documentation in your vault
3. **Searching for Information**: Augment can search your vault for relevant information

### Example Prompts

- "Create a task to document the API endpoints for the project"
- "Update the documentation for the authentication system"
- "Find information about the database schema in my vault"

## Best Practices

1. **Be Specific**: Provide clear, specific instructions to get the best results
2. **Review Changes**: Always review changes made by Augment before marking tasks as complete
3. **Provide Context**: Give Augment context about what you're trying to accomplish
4. **Use Task IDs**: Reference task IDs when asking Augment to work on specific tasks
5. **Incremental Changes**: For complex tasks, break them down into smaller steps

## Troubleshooting

- **Connection Issues**: Make sure the MCP server is running and the API key is correct
- **Permission Errors**: Ensure the MCP server has permission to access your Obsidian vault
- **Task Not Found**: Check that you're using the correct task ID
- **File Not Found**: Verify that file paths are correct and use the proper format

## Additional Resources

- [Augment Documentation](https://www.augmentcode.ai/)
- [Claude Documentation](https://docs.anthropic.com/claude/)
- [Obsidian Local REST API Documentation](https://github.com/coddingtonbear/obsidian-local-rest-api)