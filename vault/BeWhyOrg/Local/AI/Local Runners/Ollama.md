# Introduction

- Type: Local LLM runner.
- Details: Ollama runs models like LLaMA and Mistral locally with an OpenAI-compatible API (e.g., http://localhost:11434). Cline can connect to Ollama’s endpoint.
- Free Option: Ollama is free and open-source, but like LMStudio, it requires hardware you don’t have yet (e.g., 8GB VRAM for LLaMA 3 8B).

Follow along: [Installation](https://youtu.be/Wjrdr0NU4Sk?si=LgA02dIxccNcD6GR)
	This demo, includes WebUi (Docker) Tutorial

## 1. Install Ollama
```bash
carlos@bewhyorg-main:~$ nvcc --version
Command 'nvcc' not found, but can be installed with:
sudo apt install nvidia-cuda-toolkit

curl -fsSL https://ollama.com/install.sh | sh
```

## 2. Pull Model and Run Model

We are using a smaller model to starting conditions

```bash
ollama pull phi3
ollama run phi3
```

- This starts the model and opens a chat interface. You can test it directly by typing “Hello world” to confirm it works.

## 3. Local Interface

### WebUI

If I want to use [[Claude.ai]] (or other LLM) instead of Ollama could install LiteLLM Proxy Server (LLM Gateway), if we want a pipeline to ask to several LLMs

### MSTY

- [msty](https://msty.app/)
	- [Video Tutorial](https://www.youtube.com/watch?v=5U_lOjfZiXg)

## 4.Configure Cline to Use Ollama:

- In Cline’s settings (Ctrl+Shift+P > “Continue: Settings”), set the API provider to “OpenAI Compatible.”

    - Enter:
        - Base URL: http://localhost:11434/v1
        - API Key: Leave blank (Ollama doesn’t require one for local use).
        - Model: phi3.

### Test with MCP
    - Ensure your Obsidian MCP server is running:

```bash
cd ~/MPCs/obsidian-mcp-server
npm start
```

- In Cline, ask: “List all tags in my Obsidian vault.” Since it’s running locally, there are no token limits or TPM restrictions.
