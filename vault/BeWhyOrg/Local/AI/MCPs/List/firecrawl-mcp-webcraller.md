# Firecrawl MCP Server

## Setup

	Run via Docker

```bash
docker pull mendableai/firecrawl-mcp-server
docker run -d -p 3000:3000 --name firecrawl-mcp mendableai/firecrawl-mcp-server
```

## Add to Cline

Global settings (~/.config/Code/User/settings.json), but follow interface or remake, `obsidian-mcp-server`same condition and has 2 solution too.


```json
{
  "mcpServers": {
	"firecrawl-mcp": {
	  "command": "docker",
	  "args": ["exec", "firecrawl-mcp", "npx", "-y", "firecrawl-mcp"],
	  "env": {}
	}
  }
}
```


## Features

- Specialized for web scraping, converts web content to LLM-friendly Markdown.
- Tools: firecrawl_scrape, firecrawl_search, firecrawl_crawl.
- Free to self-host, or use their cloud API (free tier: 2000 credits, ~$0.50 worth of usage).

## Limitations
- Docker setup is slightly more complex than Anthropic’s Node.js server.
- Cloud API has credit limits (2000 credits), but self-hosting avoids this.


## Comparison

- Ease of Use: Anthropic’s WebCrawler is simpler to set up (Node.js vs. Docker), but Firecrawl’s Markdown output is more LLM-friendly.
- Performance: Firecrawl is faster and more robust for scraping (e.g., handles dynamic sites better), while Puppeteer can be slower and less reliable.
- MCP Suitability: Firecrawl is better for your use case, as its Markdown output reduces token usage (LLMs process Markdown more efficiently than raw HTML).
- Cost: Both are free to self-host, but Firecrawl’s cloud API has limits.

## Recommendation

- Use Firecrawl MCP for web scraping tasks. It’s more efficient for your LLM (less token usage due to Markdown) and better suited for scraping complex sites.
- Test it in Cline with Vertex AI:
    - Ask: “Scrape [https://example.com](https://example.com) and summarize it.”
    - Document the results in Obsidian (MCP-WebCrawler-Testing.md).
