# Introduction

**Status**: Mixed—offers an API (500K tokens/month free tier, but paid beyond that, e.g., $1.10/million output tokens in Cline) and can be run locally (open-source models like DeepSeek-V3, DeepSeek-R1).
**Local Deployment**: Possible with sufficient hardware (e.g., DeepSeek R1 14B requires 16GB VRAM at FP16, ~10GB at 4-bit). You’re targeting this model for your future GPU upgrade.
**Priority**: High for local deployment. DeepSeek R1 is your target model once you upgrade your GPU, and you can test smaller DeepSeek models (if available) with Ollama now.

## Known Versions

|             | Parameters | VRAM | Quantization | -    |
| ----------- | ---------- | ---- | ------------ | ---- |
| DeepSeek-R1 | 14B        | 10GB | INT8         | 86.7 |
| DeepSeek-R1 | 14B        | 16GB | FP16         | 86.7 |

## List Available Models In Cline

But can change, and the mixed options (OpenAi Compatible), this would be the access to remote API, for local ollama runner, next chapter.
### deepseek-chat
Max output: 8,000 tokens  
Cache writes price: $0.27/million tokens  
Cache reads price: $0.07/million tokens  
Output price: $1.10/million tokens
### deepseek-reasoner
Max output: 8,000 tokens  
Cache writes price: $0.55/million tokens  
Cache reads price: $0.14/million tokens  
Output price: $2.19/million tokens

## Bad Take on V3 vs R1

A short intro, the model will move info around, and there will be more reports in hardware.

### DeepSeek-V3

- A 671B parameter Mixture-of-Experts (MoE) model with 37B active parameters per token, released in late 2024. It has a 128K token context window and excels in reasoning, coding, and math tasks.
- DeepSeek-V3 scores 78% on MMLU-Pro CS (per a 2025 benchmark), matching Qwen2.5 72B but falling short of top models like QwQ 32B (79%). It’s strong in reasoning and coding, with a 128K token context window, making it better suited for MCP tasks that involve large Obsidian files or long contexts.
- It excels in math (e.g., high scores on MMLU and HumanEval) and coding, which could be useful if your Obsidian documentation involves technical content or code snippets.
- Context window: 128K tokens. This is much better for MCP tasks, as you can process entire Obsidian files or maintain long conversations without truncation.
- DeepSeek’s free tier (via their API) offers 500K tokens/month, but MCP tasks (e.g., reading a large file, appending content) can burn through this quickly, especially with a 128K context window.

### DeepSeek-R1

- Also a 671B parameter MoE model, released in January 2025, focused on reasoning via reinforcement learning (RL). It has a 128K token context window and performs well in math, coding, and structured reasoning.
- DeepSeek-R1 (and its distilled version, DeepSeek-R1-Distill-Llama-70B) is a reasoning-focused model. The distilled version on Groq scores 94.5% on MATH-500 and 86.7% on AIME 2024, outperforming OpenAI’s o1-mini and GPT-4o in math (65.2% on GPQA Diamond, 57.5% on LiveCodeBench).
- It’s designed for chain-of-thought (CoT) reasoning, which is ideal for MCP tasks requiring structured problem-solving (e.g., summarizing Obsidian notes or generating new content based on existing documentation).
- Context window: 128K tokens (same as DeepSeek-V3). The distilled version on Groq has a 130K token window, per some analyses.
- On Groq, it benefits from the same free tier (60 requests/minute), but its larger context window makes it more suitable for MCP tasks without needing to chunk data.

