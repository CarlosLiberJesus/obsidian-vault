# Introduction

**Status**: You noted that other Chinese LLMs (e.g., Alibaba Qwen) aren’t locally run or “buzzed for quality,” but Qwen ranks well in open-source benchmarks.
**Local Deployment**: Possible—Qwen 1.5 4B (~4.5GB VRAM at 4-bit) can run on your GTX 1660 SUPER, and larger models like Qwen 72B require ~40GB VRAM at FP16, ~20GB at 4-bit.
**Priority**: Medium. Qwen 1.5 4B is a good option to test locally with Ollama, and its performance (e.g., ~71% on MMLU) is comparable to Phi-3 Mini.

## Known Versions

|          | Parameters | VRAM  | Quantization | -   |
| -------- | ---------- | ----- | ------------ | --- |
| Qwen 1.5 | 4B         | 4.5GB | INT4         | 70  |
| Qwen 1.5 | 4B         | 4.5GB | INT8         | 70  |
| Qwen 1.5 | 4B         | 8GB   | FP16         | 71  |
| Qwen 1.5 | 72B        | 40GB  | INT8         | -   |
| Qwen 1.5 | 72B        | 80GB  | FP16         | -   |

