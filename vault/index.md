# Dear Future AI Assistant,

Welcome to the BeWhyOrg project vault! 🌟

You're about to embark on a fascinating journey through Portugal's civic history. This project aims to map the intricate web of citizens, institutions, and governments from 1736 (Monarquia Absoluta) to the present day. Think of it as a digital time machine that preserves and connects the threads of our democratic fabric.

## What Makes This Project Special

We're not just building a database - we're crafting a living memory of how Portuguese democracy evolved. Every citizen, every position, every institutional change tells part of a greater story. Your role is to help us maintain and enhance this digital tapestry with precision and care.

## Our Philosophy

"O código liberta... Programa-mos uma cidadania reforçada."
(Code liberates... We program strengthened citizenship.)

We believe in:
- Precision in historical documentation
- Clarity in relationship mapping
- Respect for temporal context
- Evolution through collaboration

## Vault Structure and Organization

```
vault/
├── BeWhyOrg/           # Trademark Holder
│   ├── Documentation/  # Public project documentation 
│   ├── InServer/       # Server-side components
│   ├── Local/          # Local development
│   └── Estado/         # Portuguese State analysis
├── Private/            # Git-ignored personal notes
├── Logs/               # Progress tracking
├── Template/           # Documentation templates
└── assets/             # Media files
```

## Best Practices for AI Assistants

### Code Intervention Guidelines

1. **Component Management**
   - Create new components instead of expanding existing ones
   - Break large components (>280 LOC) into smaller, manageable pieces
   - Follow established patterns in [[BeWhyOrg/Local/Tech-Stack/Laravel|Laravel]] and [[BeWhyOrg/Local/Tech-Stack/Angular|Angular]]

2. **Data Quality Checks**
   - Verify source data integrity
   - Ensure consistent field capture
   - Standardize date/time formats
   - Maintain numeric precision
   - Handle character encoding correctly

3. **Documentation Standards**
   - Use proper file naming conventions (kebab-case for files)
   - Include appropriate metadata in frontmatter
   - Maintain consistent heading hierarchy
   - Link related documents using wiki-links

### Metadata Standards

Use YAML frontmatter at the start of documents:

```yaml
---
title: Document Title
created: YYYY-MM-DD
type: [documentation, guide, task, etc]
tags: [relevant, tags]
status: [draft, review, complete]
---
```

### Security and Maintenance

1. **Security Practices**
   - Store sensitive information in `Private/` directory
   - Never include credentials in public docs
   - Use placeholders for sensitive data

2. **Maintenance Tasks**
   - Update broken links
   - Review and update documentation
   - Archive outdated content
   - Maintain consistent formatting

## Working with Tasks

Use the Obsidian Tasks plugin for managing interventions:
- Follow task creation guidelines
- Use proper status markers
- Create appropriate task logs

## Quality Assurance

When working with code or data:

### Transformation Checks
- [ ] Data normalization rules applied consistently
- [ ] Reference data integrity maintained
- [ ] Business rules correctly implemented
- [ ] Edge cases handled (nulls, empty strings, etc.)
- [ ] Duplicate detection/handling strategy

### Code Review Process
- Verify alignment with existing patterns
- Check for proper error handling
- Ensure documentation is updated
- Validate test coverage

## Final Notes

Remember: You're not just processing data - you're helping preserve and understand the evolution of Portuguese democracy. Every change you suggest, every improvement you make contributes to this historical documentation project.

Use the available tools wisely:
- Search functionality for finding relevant information
- Templates for consistent documentation
- Version control for tracking changes
- Task management for organized workflows
- Don't forget to check [[BeWhyOrg/Local/AI/MCPs/Obsidian-MCP-Actions/README|Obsidian-MCP-Actions]], server should be up ;) 

Let's work together to make this project even better!

With anticipation for our collaboration,
The BeWhyOrg Team