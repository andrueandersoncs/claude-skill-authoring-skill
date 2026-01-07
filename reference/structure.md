# Skill Structure Patterns

## Progressive Disclosure

SKILL.md is a table of contents pointing to detailed materials. Claude loads reference files only when needed.

### Pattern 1: High-level guide with references

```markdown
# PDF Processing

## Quick start
\`\`\`python
import pdfplumber
with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
\`\`\`

## Advanced features
**Form filling**: See [FORMS.md](FORMS.md)
**API reference**: See [REFERENCE.md](REFERENCE.md)
**Examples**: See [EXAMPLES.md](EXAMPLES.md)
```

### Pattern 2: Domain-specific organization

For skills with multiple domains, organize by domain:

```
bigquery-skill/
├── SKILL.md (overview and navigation)
└── reference/
    ├── finance.md (revenue, billing)
    ├── sales.md (pipeline, accounts)
    ├── product.md (usage, features)
    └── marketing.md (campaigns)
```

```markdown
# BigQuery Analysis

## Available datasets
**Finance**: Revenue, ARR → See [reference/finance.md](reference/finance.md)
**Sales**: Pipeline, accounts → See [reference/sales.md](reference/sales.md)

## Quick search
\`\`\`bash
grep -i "revenue" reference/finance.md
\`\`\`
```

### Pattern 3: Conditional details

Show basic content, link to advanced:

```markdown
## Creating documents
Use docx-js. See [DOCX-JS.md](DOCX-JS.md).

## Editing documents
For simple edits, modify XML directly.
**For tracked changes**: See [REDLINING.md](REDLINING.md)
```

## File Organization Guidelines

### Reference file structure

For files over 100 lines, include a table of contents:

```markdown
# API Reference

## Contents
- Authentication and setup
- Core methods (create, read, update, delete)
- Advanced features
- Error handling
- Code examples

## Authentication and setup
...
```

### Naming files

Use descriptive names:
- **Good**: `form_validation_rules.md`, `finance_metrics.md`
- **Bad**: `doc2.md`, `file1.md`

### Path conventions

Always use forward slashes: `reference/guide.md`
Never use backslashes: `reference\guide.md`

## What Goes Where

### In SKILL.md (loaded when triggered)
- Frontmatter with name and description
- Quick start / most common use case
- Navigation to reference files
- Core rules that always apply

### In reference files (loaded as needed)
- Complete API documentation
- Extensive examples
- Domain-specific schemas
- Edge cases and advanced features

### As executable scripts (executed, not loaded)
- Validation scripts
- Data processing utilities
- Format conversion tools

Scripts consume tokens only for output, not source code.
