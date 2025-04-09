# Introduction

- Type: Local LLM runner.
- Details: Ollama runs models like LLaMA and Mistral locally with an OpenAI-compatible API (e.g., http://localhost:11434). Cline can connect to Ollama’s endpoint.
- Free Option: Ollama is free and open-source, but like LMStudio, it requires hardware you don’t have yet (e.g., 8GB VRAM for LLaMA 3 8B).

1. Install Ollama:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

2. Pull Phi-3 Mini:
```bash
ollama pull phi3
```

- This downloads the 4-bit quantized version by default (~4GB), which should fit in your VRAM.

3. Run Ollama:
    ```bash
    ollama run phi3
    ```

- This starts the model and opens a chat interface. You can test it directly by typing “Hello world” to confirm it works.

4. Configure Cline to Use Ollama:

- In Cline’s settings (Ctrl+Shift+P > “Continue: Settings”), set the API provider to “OpenAI Compatible.”

    - Enter:
        - Base URL: http://localhost:11434/v1
        - API Key: Leave blank (Ollama doesn’t require one for local use).
        - Model: phi3.

5. Test with MCP:
    - Ensure your Obsidian MCP server is running:

```bash
cd ~/IDEs/obsidian-mcp-server
npm start
```

- In Cline, ask: “List all tags in my Obsidian vault.” Since it’s running locally, there are no token limits or TPM restrictions.


Why This Works:

- Running Phi-3 Mini locally with Ollama bypasses remote API token limits (like Groq’s 6000 TPM or Vertex AI’s credit limits).
- Your 6GB VRAM can handle Phi-3 Mini at 4-bit quantization, and your good CPU/DDR5 RAM will help with preprocessing and inference.