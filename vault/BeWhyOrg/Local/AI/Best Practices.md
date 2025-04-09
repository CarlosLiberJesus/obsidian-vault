# Ideias for best practices

- In [[Cline]] already have some context, but all Agents should have a best practices/custom instructions to apply;
	- in future there should be a custom workflow between my prompt LLM and MCPs until response
- "if you need to update an existing component, instead of adding more code inside, create a new one. And do your best to break larges (> 280 LOC) you're about to edit into smaller, manageable ones"
- having more flows like [[BeWhyOrg/Local/Tech-Stack/Laravel|Laravel]] and [[BeWhyOrg/Local/Tech-Stack/Angular|Angular]] 


## Code Review Checklist and Process

### Quick Review Process

1. **Scan for critical issues** (2-3 min)
    - Security vulnerabilities
    - Performance bottlenecks
    - Build/compilation errors
2. **Review code functionality** (5-10 min)
    - Does it meet requirements?
    - Are edge cases handled?
    - Is there appropriate error handling?
3. **Review code quality** (5-10 min)
    - Is the code maintainable?
    - Is it properly documented?
    - Does it follow project standards?
4. **Provide feedback** (3-5 min)
    - Prioritize issues (critical, important, nice-to-have)
    - Be specific and constructive
    - Include examples when helpful

### Detailed Checklist

### Functionality

- [ ]  Code fulfills the intended requirements
- [ ]  Edge cases are handled appropriately
- [ ]  Error handling is comprehensive and graceful
- [ ]  All functions return expected outputs
- [ ]  Changes don't break existing functionality

### Security

- [ ]  Input validation is present and appropriate
- [ ]  Authentication/authorization checks in place
- [ ]  No sensitive data exposed in logs or responses
- [ ]  SQL injection and XSS protections
- [ ]  No hardcoded secrets or credentials

### Performance

- [ ]  Efficient algorithms and data structures
- [ ]  No redundant computations
- [ ]  Appropriate caching strategies
- [ ]  Database queries are optimized
- [ ]  No N+1 query problems

### Readability & Maintainability

- [ ]  Clear, descriptive variable/function names
- [ ]  Functions have single responsibility
- [ ]  DRY (Don't Repeat Yourself) principle followed
- [ ]  Consistent formatting and style
- [ ]  Complex logic includes comments explaining "why"

### Testing

- [ ]  Unit tests cover critical paths
- [ ]  Edge cases are tested
- [ ]  Tests are readable and maintainable
- [ ]  Test coverage is adequate

### Documentation

- [ ]  Public APIs documented
- [ ]  Comments for complex sections
- [ ]  README updated if needed
- [ ]  Changelog updated if applicable

## Time-Saving Tips

1. **Prioritize review items** based on risk and impact
2. **Use automated tools** for style/lint checking
3. **Focus on business-critical sections** first
4. **Create templates** for common feedback
5. **Schedule dedicated review time** blocks

## Constructive Feedback Guidelines

- Be specific about what and why, not just what's wrong
- Suggest improvements, not just identify problems
- Use "we" language instead of "you" when possible
- Ask questions to understand rationale
- Recognize good patterns and practices

## Review Comment Templates

### For Suggestions

"Consider using [alternative approach] here because [reason]."

### For Questions

"What was the reasoning behind [decision]? I'm wondering if [alternative] might work better because [reason]."

### For Critical Issues

"This might lead to [specific problem]. We should address this by [suggestion]."