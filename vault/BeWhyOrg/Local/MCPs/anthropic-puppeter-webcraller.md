# Anthropic WebCrawler MCP


## Clone Anthropic Puppeteer MCP server

```bash
git clone https://github.com/anthropic-ai/mcp-puppeteer.git ~/MCPs/mcp-puppeteer
cd ~/MCPs/mcp-puppeteer
npm install
npm run build
```

	Run

Watch for ports mapping. default also 3000 or 4200 due to npm

```bash
npm start --port=
```


## Add to Cline

Global settings (~/.config/Code/User/settings.json), but follow interface or remake, `obsidian-mcp-server`same condition and has 2 solution too.

```json
{
  "mcpServers": {
	"puppeteer-mcp-server": {
	  "command": "node",
	  "args": ["/home/carlos/IDEs/mcp-puppeteer/build/index.js"],
	  "env": {}
	}
  }
}
```


## Features

- Uses Puppeteer to scrape websites, execute JavaScript, and return HTML or text.
- Tools: puppeteer_get_page_content, puppeteer_navigate, puppeteer_screenshot.
- Free to self-host, no API costs.

## Limitations

- Requires local setup and maintenance (e.g., handling Puppeteer dependencies like Chromium).
- Slower for complex sites due to Puppeteer’s overhead.
- No built-in Markdown conversion (returns raw HTML).

