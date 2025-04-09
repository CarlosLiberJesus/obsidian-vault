# Introduction

**Status**: Open-source model by Google. Gemma 2B (~2GB VRAM at 4-bit) can run on your GPU, and Gemma 9B requires ~6GB VRAM at 4-bit.
**Local Deployment**: Possible—Gemma 2B is a lightweight option for your current setup.
**Priority**: Medium. Gemma 2B is a fallback if Phi-3 Mini or Qwen 1.5 4B don’t perform well.

## Known Versions

|       | Parameters | VRAM | Quantization | -   |
| ----- | ---------- | ---- | ------------ | --- |
| Gemma | 2B         | 2GB  | INT8         | 65  |
| Gemma | 2B         | 4GB  | FP16         | 65  |
| Gemma | 9B         | 6GB  | INT8         | 78  |
| Gemma | 9B         | 12GB | FP16         | 78  |
