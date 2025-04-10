# Best Practices for Code Interventions with LLMs

This file provides custom instructions and guidelines for Large Language Models (LLMs) during code interventions. It outlines best practices for ensuring the quality, maintainability, and security of code generated or modified by LLMs.

## Choosing an LLM

When selecting an LLM for code interventions, consider the following factors:

*   **Local vs. API-based**: Local LLMs like Phi-3 Mini and Qwen 1.5 offer privacy, cost savings, and reduced reliance on external APIs. API-based LLMs like Claude and Gemini may offer better performance but come with usage costs and potential privacy concerns.
*   **Task requirements**: Choose an LLM that is well-suited for the specific task. For example, DeepSeek is known for its strong coding and reasoning abilities, while other models may excel at natural language processing.
*   **Hardware constraints**: Ensure that the LLM can run on your available hardware. Smaller models like Phi-3 Mini and Qwen 1.5 4B can run on modest GPUs, while larger models require more powerful hardware.

Refer to the [[LLM Review]] note for more information on available LLMs and their capabilities.

## Task Management

Use the Obsidian Tasks plugin to manage code interventions with LLMs. The [[Task Creation Tutorial]] note provides detailed instructions on how to create and use tasks for this purpose.

## Data Quality Checks

When integrating data from external sources or transforming existing data, perform the following data quality checks:

### Extraction Phase

- [ ]  Source data integrity verified
- [ ]  All required fields captured
- [ ]  Character encoding handled correctly
- [ ]  Date/time formats standardized
- [ ]  Numeric precision maintained

### Transformation Checks

- [ ]  Data normalization rules applied consistently
- [ ]  Reference data integrity maintained
- [ ]  Business rules correctly implemented
- [ ]  Edge cases handled (nulls, empty strings, etc.)
- [ ]  Duplicate detection/handling strategy

These checks are based on the best practices outlined in the [[BeWhyOrg/Local/Tech-Stack/Laravel|Laravel]] and [[BeWhyOrg/Local/Tech-Stack/Angular|Angular]] notes.

## Code Review Checklist and Process

- In [[Cline]] already have some context, but all Agents should have a best practices/custom instructions to apply;
	- in future there should be a custom workflow between my prompt LLM and MCPs until response
- "if you need to update an existing component, instead of adding more code inside, create a new one. And do your best to break larges (> 280 LOC) you're about to edit into smaller, manageable ones"
- having more flows like [[BeWhyOrg/Local/Tech-Stack/Laravel|Laravel]] and [[BeWhyOrg/Local/Tech-Stack/Angular|Angular]]
