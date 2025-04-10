# Introduction

**Status**: You listed Mistral twice, first noting “only API to run local” (likely referring to Cline’s paid API integration, e.g., Mistral Large at $6/million output tokens), then “run local” (correct—Mistral models are open-source).
**Local Deployment**: Possible—Mistral 7B (~4GB VRAM at 4-bit) can run on your GTX 1660 SUPER, and Mistral Large 2 (128K token context window) requires ~16GB VRAM at FP16, ~10GB at 4-bit.
**Priority**: High for local deployment. You can test Mistral 7B with Ollama now, and Mistral Large 2 is another option for your future GPU upgrade.

## Known Versions

|                 | Parameters | VRAM | Quantization | -   |
| --------------- | ---------- | ---- | ------------ | --- |
| Mistral         | 7B         | 4GB  | INT8         | -   |
| Mistral         | 7B         | 8GB  | FP16         | -   |
| Mistral Large 2 | 70B        | 16GB | INT8         | -   |
| Mistral Large 2 | 70B        | 32GB | FP16         | -   |

## List Available Cline Models

Again probably payed, we are in the local business.
### mistral-large-2411
Max output: 131,000 tokens  
Input price: $2.00/million tokens  
Output price: $6.00/million tokens
### mistral-3b-2410
Max output: 131,000 tokens  
Input price: $0.04/million tokens  
Output price: $0.04/million tokens
### mistral-8b-2410
Max output: 131,000 tokens  
Input price: $0.10/million tokens  
Output price: $0.10/million tokens
### mistral-small-latest
Max output: 131,000 tokens  
Input price: $0.10/million tokens  
Output price: $0.30/million tokens
### open-codestral-mamba
Max output: 256,000 tokens  
Input price: $0.15/million tokens  
Output price: $0.15/million tokens



