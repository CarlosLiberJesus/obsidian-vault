# Introduction

This file will help to map which RTX to buy, based also on [[LLM Theory]]; In [[LLM Review]] we have a list of local models, which each will try to have it's own parity of VRAM. 

## Current Set-Up

GeForce GTX 1660 SUPER - 6GB

Lucky to Run [[Ollama]] with:

- Phi-3 Mini (3.8B parameters):
    - VRAM Requirement: ~4GB at 4-bit quantization, ~6GB at 8-bit.
    - Performance: Good for basic tasks (e.g., text generation, simple reasoning). Scores ~70% on MMLU (general knowledge benchmark), suitable for MCP tasks like listing tags or appending to Obsidian files.
        
- Gemma 2B (2B parameters):
    - VRAM Requirement: ~2GB at 4-bit quantization, ~3GB at 8-bit.
    - Performance: Slightly weaker than Phi-3 Mini (~65% on MMLU), but very lightweight and fast on your GPU.
        
- Qwen 1.5 4B (4B parameters):
    - VRAM Requirement: ~4.5GB at 4-bit quantization, ~6.5GB at 8-bit.
    - Performance: Comparable to Phi-3 Mini (~71% on MMLU), with better multilingual support if your Obsidian notes include non-English content.
- Mistral 7B 
	- (~4GB VRAM at 4-bit) 
- LLaMA 3.2 3B at FP16 or LLaMA 3.1 8B at 4-bit (~5GB VRAM)


## 6GB and 16GB VRAM Ranges

You specifically asked about models fitting within 6GB and 16GB VRAM. Here’s a focused list based on the table:

### 6GB VRAM Range

These models fit within 6GB, primarily at INT8 quantization:

- Phi-3 Mini (3.8B, 4GB, INT8): Compact and efficient, good for lightweight tasks.
- Qwen 1.5 (4B, 4.5GB, INT8): Scores 70, solid for general-purpose use.
- LLaMA 3.1 (8B, 5GB, INT8): Scores 80, a strong contender for its size.
- Gemma (9B, 6GB, INT8): Scores 78, excellent for slightly larger tasks.
- Mistral (7B, 4GB, INT8): Versatile and widely used.

### 16GB VRAM Range

These models fit within 16GB, using either FP16 or INT8:

- DeepSeek-R1 (14B, 10GB INT8 or 16GB FP16): Scores 86.7, high-performing for research or complex tasks.
- Phi-4 (14B, 10GB INT8 or 16GB FP16): A balanced option for mid-range setups.
- Mistral Large 2 (70B, 16GB INT8): Large-scale model accessible with INT8 quantization.
- LLaMA 3.1 (8B, 10GB FP16): Scores 80, viable with higher precision.


## GPU Table Options

|VRAM Tier|Model|Parameters|VRAM (4-bit)|VRAM (FP16)|Notes|
|---|---|---|---|---|---|
|2–4GB|Gemma 2B|2B|~2GB|~4GB|Lightweight, fast, ~65% MMLU. Runs easily on your 6GB GPU.|
||LLaMA 3.2 1B|1B|~2GB|~4GB|Smallest LLaMA, basic tasks, fits your 6GB GPU.|
|4–6GB|Phi-3 Mini|3.8B|~4GB|~8GB|~70% MMLU, good for MCP tasks (e.g., listing Obsidian tags).|
||Qwen 1.5 4B|4B|~4.5GB|~8GB|~71% MMLU, multilingual support, works on your 6GB GPU at 4-bit.|
||LLaMA 3.2 3B|3B|~3GB|~6GB|Slightly better than Gemma 2B, fits your 6GB GPU.|
||LLaMA 3.1 8B|8B|~5GB|~10GB|~80% MMLU, strong for its size, just fits your 6GB GPU at 4-bit.|
|6–10GB|Gemma 9B|9B|~6GB|~12GB|~78% MMLU, requires a small VRAM upgrade from your 6GB.|
|10–16GB|DeepSeek-R1 14B|14B|~10GB|~16GB|Excellent reasoning (86.7% AIME 2024), target for 16GB VRAM.|
||Phi-4 14B|14B|~10GB|~16GB|Next-gen Phi, ~82% MMLU, needs 16GB VRAM for FP16.|
||Qwen 1.5 14B|14B|~10GB|~16GB|Multilingual, ~83% MMLU, good for 16GB VRAM.|
|16–24GB|None in this range|-|-|-|Models jump from 16GB to higher tiers.|
|24GB+|LLaMA 3.1 70B|70B|~40GB|~80GB|High performance, needs 24GB+ at 4-bit (multi-GPU recommended).|
||Qwen 72B|72B|~40GB|~80GB|Similar to LLaMA 3.1 70B, requires significant VRAM.|
||LLaMA 3.1 405B|405B|~240GB|~480GB|Massive model, needs a GPU cluster (e.g., 8x 80GB GPUs).|






