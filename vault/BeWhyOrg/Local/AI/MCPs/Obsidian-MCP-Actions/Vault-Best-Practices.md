# Obsidian Vault Best Practices

## File Naming Conventions

1. **Use Hyphens**: 
   - Use hyphens (-) instead of spaces
   - Example: `Task-Management.md` not `Task Management.md`

2. **Case Sensitivity**:
   - Use PascalCase for main folders: `BeWhyOrg/`, `Private/`, `Logs/`
   - Use kebab-case for files: `vault-best-practices.md`

3. **File Extensions**:
   - Always include `.md` extension for markdown files
   - Use appropriate extensions for assets (`.png`, `.jpg`, etc.)

## Folder Structure

```
vault/
├── BeWhyOrg/           # Public project documentation
│   ├── InServer/       # Server-side components
│   ├── Local/          # Local development
│   └── Estado/         # Portuguese State analysis
├── Private/            # Git-ignored personal notes
├── Logs/               # Progress tracking
├── Template/           # Documentation templates
└── assets/             # Media files
```

## LLM Guidelines

1. **File Creation**:
   - Always use hyphens instead of spaces
   - Create files in appropriate directories based on content type
   - Include proper frontmatter with metadata

2. **Content Organization**:
   - Use consistent heading levels (H1 for title, H2 for main sections)
   - Include table of contents for longer documents
   - Link related documents using wiki-links [[document-name]]

3. **Task Management**:
   - Follow Task-Management.md guidelines for task creation
   - Use proper task format and status markers
   - Create task logs in `Logs/Tasks/`

4. **Logging**:
   - Use `Logs/Daily-Logs/` for daily activities
   - Use `Logs/Weekly-Logs/` for weekly summaries
   - Never delete existing log content, only append

## Metadata Standards

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

## Link Management

1. **Internal Links**:
   - Use wiki-links: [[document-name]]
   - Include heading when linking to specific section: [[document-name#section]]

2. **External Links**:
   - Use markdown links: [text](url)
   - Include reference links for repeated URLs

## Asset Management

1. **Image Storage**:
   - Store in `assets/` directory
   - Use subdirectories for organization
   - Use descriptive filenames

2. **File Types**:
   - Images: PNG, JPG, SVG
   - Documents: PDF, MD
   - Data: JSON, YAML

## Version Control

1. **Git Integration**:
   - Ignore `Private/` directory
   - Commit regular snapshots of public documentation
   - Use meaningful commit messages

## Search and Tags

1. **Tagging System**:
   - Use hierarchical tags: #category/subcategory
   - Maintain consistent tag vocabulary
   - Document common tags

2. **Search Terms**:
   - Include relevant keywords in headers
   - Use consistent terminology
   - Add aliases for common terms

## Template Usage

1. **Standard Templates**:
   - Use templates from `Template/` directory
   - Follow template structure
   - Include required metadata

## Security

1. **Sensitive Information**:
   - Store in `Private/` directory
   - Never include credentials in public docs
   - Use placeholders for sensitive data

## Maintenance

1. **Regular Tasks**:
   - Update broken links
   - Review and update documentation
   - Archive outdated content
   - Maintain consistent formatting