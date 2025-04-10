# Introduction

A File to review concept on how to calculate and pick the model. We already concluded, as dev, 16GB is the right place to start before scalling. This file may reference impossible set up, but we will learn has we go alot

## Name-splaning 



## Quantization

- FP32 (Full Precision): Highest quality, largest size.
- FP16 (Half Precision): Half the size, 0–2% quality loss.
- INT8 (8-bit): 4x smaller, 1–3% quality loss.
- INT4 (4-bit): 8x smaller, 10–30% quality loss. This aligns with our discussion on 

### Diff between FT16 and INT8

To address your question: “So models are both FP and INT, or INT8 lower level nem FP?” Models can technically run at either FP (like FP32 or FP16) or INT (like INT8) precisions, depending on how they’re quantized. FP16 is a “higher” precision than INT8 because it retains more quality (only 0–2% loss vs. 1–3% for INT8), but INT8 uses less VRAM (4x smaller than FP32 vs. 2x for FP16). YouTube tutorials can dive deeper into quantization if you want more details, but for now, we’ll focus on FP16 and INT8 as your preferred options.

### FP16 vs. INT8: Why FP16 Might Be Preferred

You asked whether FP16 is a better choice than INT8 despite their differences in quantization. Here’s the breakdown:

- FP16 (16-bit Floating Point): Retains more precision, typically resulting in minimal quality loss (0–2% compared to full-precision models). It’s preferred for tasks where accuracy is critical, like natural language understanding or generation, assuming you have sufficient VRAM.
- INT8 (8-bit Integer): Reduces VRAM usage significantly (often by half compared to FP16) but introduces slightly more quality loss (1–3%). It’s a great option when VRAM is limited or when speed is a priority over marginal accuracy gains.

Conclusion: FP16 is generally the better choice if your hardware can handle the VRAM requirements (e.g., 8GB+ for smaller models). INT8 becomes preferable in constrained environments (e.g., 6GB VRAM), balancing performance and resource use. For most modern models on platforms like Ollama, both are optimized well, so the choice depends on your setup.

### Why No FP32?

You noted the absence of FP32 (32-bit Floating Point). Here’s why it’s excluded:
- VRAM Demand: FP32 doubles FP16’s memory usage (e.g., a 7B model in FP16 uses 8GB, but FP32 would need 16GB+), making it impractical for most local setups, even with older or smaller models.
- Practicality: For inference (not training), FP32 offers negligible accuracy gains over FP16, so it’s rarely supported in tools like Ollama unless precision is mission-critical (e.g., scientific applications).

If you need FP32, older models like GPT-2 (1.5B) might fit in 6GB, but modern frameworks prioritize FP16/INT8 for efficiency.

## Parameters

Parameters are the internal settings or "knowledge" an LLM learns during training. Think of them as the connections in the model’s "brain" (a neural network). Each parameter is a number that helps the model predict the next word or understand language patterns.

- Example: A model like LLaMA 3.1 8B has 8 billion parameters—basically 8 billion tiny adjustments that let it understand and generate text.

### Areas of Training?

Parameters are learned during the training process, which involves feeding the model massive amounts of text data (e.g., books, websites, code). The "areas" of training refer to the types of data and tasks the model is exposed to:

- General Knowledge: Wikipedia, books, and articles to learn facts and language patterns.
- Conversational Data: Chat logs or dialogues to improve conversational skills.
- Code: GitHub repositories for coding tasks (e.g., Qwen excels at this).
- Specialized Domains: Some models are fine-tuned on specific areas like legal texts, medical data, or multilingual content (e.g., Qwen’s multilingual support).

The more parameters a model has, the more it can "learn" from these areas, but it also needs more VRAM to store and process them.

## Context Window

The context window is the amount of text (measured in tokens) an LLM can "look at" at once when generating a response or understanding a prompt. Tokens are chunks of text—roughly a word or part of a word (e.g., "hello" is one token, "unbelievable" might be two).

- Max Holding/Processing of Tokens: This is the maximum number of tokens the model can process in one go. For example:
    - LLaMA 3.1 8B: ~128K tokens.
    - Gemma 2B: ~8K tokens.
    - DeepSeek-R1 14B: ~130K tokens.

### MCP Token Count?

When using MCP (Model Context Protocol) servers (like your Obsidian MCP), the context window includes:
- The user’s prompt (e.g., “List all tags in my Obsidian vault”).
- The MCP server’s response (e.g., a list of tags or file contents).
- Any additional context (e.g., conversation history).
    

MCP tasks can increase token usage because the model needs to process both the prompt and the external data (e.g., a large Obsidian file). A larger context window (like DeepSeek-R1’s 130K tokens) is better for MCP tasks since it can handle more data without forgetting earlier parts.

### Can we add "attention"?



## What Are NLP Tasks?

NLP covers a wide range of tasks that help computers process and make sense of text or speech. Here are some key examples:

- Translation: Converting text from one language to another (e.g., English to French).
- Summarization: Taking a long piece of text and creating a shorter version with the main points.
- Question Answering: Responding to questions based on a given text or knowledge (like what I’m doing now!).
- Text Generation: Writing human-like text, such as stories or chatbot responses.
- Sentiment Analysis: Figuring out if a piece of text is positive, negative, or neutral (e.g., analyzing reviews).
    

And yes, one specific task is detecting people’s names in paragraphs, which I’ll explain next!

### Detecting People’s Names in Paragraphs: Named Entity Recognition (NER)

One cool NLP task is called Named Entity Recognition (NER). This is all about finding and identifying specific things—like names of people, places, or organizations—in a block of text. For example:

- Input Text: "Albert Einstein was born in Ulm, Germany, and worked at Princeton University."
- NER Output:
    - People: "Albert Einstein"
    - Places: "Ulm, Germany"
    - Organizations: "Princeton University"

So, if you give NLP a paragraph, it can scan through and say, "Here are all the people mentioned!" This is super useful for things like organizing data, searching documents, or even building knowledge bases.



## Compreensive Model List

| Model Name      | Parameters | VRAM  | Quantization | Context Window | Score |
| --------------- | ---------- | ----- | ------------ | -------------- | ----- |
| Qwen 1.5        | 4B         | 4.5GB | INT4         |                | 70    |
| Qwen 1.5        | 4B         | 4.5GB | INT8         |                | 70    |
| Qwen 1.5        | 4B         | 8GB   | FP16         |                | 71    |
| Qwen 1.5        | 72B        | 40GB  | INT8         |                | -     |
| Qwen 1.5        | 72B        | 80GB  | FP16         |                | -     |
| DeepSeek-R1     | 14B        | 10GB  | INT8         | 130K           | 86.7  |
| DeepSeek-R1     | 14B        | 16GB  | FP16         |                | 86.7  |
| Falcon          | 7B         | 4GB   | INT8         |                | -     |
| Falcon          | 7B         | 8GB   | FP16         |                |       |
| Mistral         | 7B         | 4GB   | INT8         |                | -     |
| Mistral         | 7B         | 8GB   | FP16         |                | -     |
| Mistral Large 2 | 70B        | 16GB  | INT8         |                | -     |
| Mistral Large 2 | 70B        | 32GB  | FP16         |                | -     |
| Gemma           | 2B         | 2GB   | INT8         | 8K             | 65    |
| Gemma           | 2B         | 4GB   | FP16         |                | 65    |
| Gemma           | 9B         | 6GB   | INT8         |                | 78    |
| Gemma           | 9B         | 12GB  | FP16         |                | 78    |
| LLaMA 3.2       | 1B         | 2GB   | INT8         |                | -     |
| LLaMA 3.2       | 1B         | 4GB   | FP16         |                | -     |
| LLaMA 3.1       | 8B         | 5GB   | INT8         | 128K           | 80    |
| LLaMA 3.1       | 8B         | 10GB  | FP16         |                | 80    |
| LLaMA 3.1       | 70B        | 40GB  | INT8         |                | -     |
| LLaMA 3.1       | 70B        | 80GB  | FP16         |                | -     |
| Phi-3 Mini      | 3.8B       | 4GB   | INT8         |                | -     |
| Phi-3 Mini      | 3.8B       | 8GB   | FP16         |                | -     |
| Phi-4           | 14B        | 10GB  | INT8         |                | -     |
| Phi-4           | 14B        | 16GB  | FP16         |                | -     |


## More documentation

- [[LLM Size, Parameters and Quantization Guide]]