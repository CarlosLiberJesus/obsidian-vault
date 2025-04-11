# Install

## 1. Enable Local Rest API

- Open Obsidian (your vault is at /mnt/local_cloud).
- Go to Settings > Community Plugins > Turn on community plugins (if not already enabled).
- Search for “Local REST API” and install it.
- Enable the plugin and note the API key it generates (you’ll need this later).
- Ensure the plugin is running (it exposes your vault via https://127.0.0.1:27124 by default).


## 2. Install the Obsidian MCP Server

```bash
git clone https://github.com/cyanheads/obsidian-mcp-server.git ~/MCPs/obsidian-mcp-server
cd ~/MCPs/obsidian-mcp-server
npm install
npm run build
```

## 3. Configure the MCP Server

```bash
nano ~/MCPs/obsidian-mcp-server/.env
```

Add:

```text
OBSIDIAN_API_KEY=your_api_key_here
VERIFY_SSL=false
OBSIDIAN_PROTOCOL=https
OBSIDIAN_HOST=127.0.0.1
OBSIDIAN_PORT=27124
```

## 4. Run the MCP Server

```bash
cd ~/MCPs/obsidian-mcp-server
npm start
```

- It should run on http://localhost:3000 by default. Keep it running in a terminal (or use screen/tmux to detach).

## 5. Try to All Agents

- Open the Command Palette: Ctrl+Shift+P.
- Type “Preferences: Open User Settings (JSON)” and select it.
- This opens ~/.config/Code/User/settings.json.

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
  }
}
```

If does not work for user, then to app?

```bash
nano ~/.vscode/mcp.json
```

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
  }
}
```

we can still try project workspace!

Continue with [[README]]