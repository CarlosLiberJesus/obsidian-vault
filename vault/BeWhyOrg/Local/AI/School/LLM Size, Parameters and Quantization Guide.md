# LLM Size, Parameters and Quantization Guide

## Model Parameters Explained

- **Parameters** in AI models represent learned knowledge - each parameter is a numerical value/weight in a neural network
- More parameters = more patterns, relationships and nuances the model can learn
- More parameters generally means "smarter" models but requires more resources to run

## Parameter Size Examples

|Model|Parameter Size|VRAM Required|GPU Example|
|---|---|---|---|
|Tiny Llama|1.1B|638MB|Very low-end/CPU|
|Llama 3.2|1B|4GB|Entry GPU|
|Llama 3.2|3B|6GB|RTX 2060|
|Llama 3.1|8B|10GB|RTX 3080 Ti|
|Microsoft Phi-3|14B|16GB|RTX 3090|
|Llama 3.3|70B|48GB|Dual 4090s|
|Llama 3.1|405B|1TB|AI cluster/H100s|
|DeepSeek|671B|~1.5TB+|Enterprise AI cluster|

## Understanding Quantization

Quantization makes large models fit on smaller GPUs by reducing precision while trying to maintain accuracy.

### Precision Types

- **FP32** - Full precision, no alterations (baseline)
- **FP16** - Half precision, 0-2% loss in precision, model half the size
- **INT8** - Integer quantization, model 4x smaller, 1-3% loss in precision
- **INT4** - Integer quantization, model 8x smaller, 10-30% loss in precision (noticeable degradation for complex tasks)

### Quantization in Model Names

- When you see notations like "GPTQ" or "Q4_K_M" in model filenames, these indicate quantization methods
- Models with "4bit" or "int4" in names are highly quantized for smaller GPUs
- "GGUF" files use newer quantization formats optimized for consumer hardware

## Running Models Locally

### For Low-End Hardware/Laptops

- Use 1B-3B parameter models
- Look for INT4/4-bit quantized versions
- Models like Llama 3.2 1B or Tiny Llama work well

### For Gaming PCs with Good GPUs

- 8B-14B models run well on RTX 3080/3090
- Can run 70B models with heavy quantization (INT4)
- Recommended: 16-24GB VRAM for good performance

### For AI Workstations/Multiple GPUs

- Can run 70B models with less quantization
- Possible to run larger models with multiple GPUs
- Memory pooling across GPUs is important

## Considerations When Choosing Models

- **Memory vs Speed**: Heavier quantization (INT4) reduces VRAM needs but slows inference
- **Quality Tradeoffs**: Smaller/more quantized models have weaker reasoning and factual accuracy
- **Use Case Matching**: Code generation needs different models than creative writing
- **Generation Speed**: Measured in tokens/sec - higher is better for interactive use

## Key Terms in Model Names

- **B**: Billions of parameters (e.g., 7B = 7 billion parameters)
- **Q4/INT4**: 4-bit quantization
- **GGUF**: New-generation quantized format for local inference
- **Instruct**: Fine-tuned for following instructions
- **Chat**: Optimized for conversational use

## Tools for Running Local Models

- **Ollama**: Easy command-line tool for running models locally
- **LM Studio**: GUI for downloading and running different models
- **XO Labs**: For clustering multiple devices
- **MLX**: Machine Learning Acceleration specifically for Apple silicon

## Continue Studies
- https://www.youtube.com/watch?v=8r9Kit3lKXE
- https://www.youtube.com/watch?v=QfFRNF5AhME

### [[Google Review]]

https://notebooklm.google.com/notebook/f8fedfae-ac22-49ad-b660-d8e2374b85e5?pli=1

