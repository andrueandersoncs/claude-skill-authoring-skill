# Claude Skill Authoring Skill

A comprehensive guide and reference for creating effective Claude Skills. This skill helps developers write well-structured, discoverable, and maintainable skills that enhance Claude's capabilities for domain-specific tasks.

## What are Claude Skills?

Claude Skills are specialized instruction sets (typically in `SKILL.md` files) that guide Claude to perform specific tasks effectively. They can include:

- Domain knowledge and terminology
- Step-by-step workflows
- Output templates and formats
- Validation patterns and error handling
- Reference files for complex topics

## Project Structure

```
claude-skill-authoring-skill/
├── SKILL.md                              # Main skill file - core principles & overview
├── SKILL_AUTHORING_BEST_PRACTICES.md     # Comprehensive authoring guide
└── reference/
    ├── structure.md                      # Progressive disclosure & organization
    ├── patterns.md                       # Common reusable patterns
    ├── advanced.md                       # Advanced executable code patterns
    └── checklist.md                      # Pre-deployment validation checklist
```

## Quick Start

1. **Read `SKILL.md`** - Start here for core principles and skill structure guidelines
2. **Explore patterns** - See `reference/patterns.md` for common skill patterns
3. **Validate your skill** - Use `reference/checklist.md` before sharing

## Core Principles

### Conciseness is Critical
Context window is shared between skills and user tasks. Only include information Claude doesn't already know.

### Degrees of Freedom
Match instruction specificity to task requirements:
- **Low freedom**: Fragile tasks needing exact output (templates, strict formats)
- **Medium freedom**: Constrained output with some flexibility (examples as guides)
- **High freedom**: Open-ended tasks (principles over prescriptions)

### Progressive Disclosure
Keep `SKILL.md` as an overview that directs to reference files for detailed information. This reduces cognitive load while maintaining completeness.

## Key Patterns

| Pattern | Use Case |
|---------|----------|
| **Template** | Exact output format required |
| **Examples** | Quality-dependent output with flexibility |
| **Workflow** | Multi-step processes with checklists |
| **Feedback Loop** | Iterative validation and correction |

## Skill Frontmatter

Every skill requires YAML frontmatter:

```yaml
---
name: processing-pdfs
description: Extracts and analyzes content from PDF documents. Use when working with PDF files, extracting text, or converting PDF content.
---
```

- **name**: Max 64 characters, lowercase with hyphens, gerund form (verb + -ing)
- **description**: Max 1024 characters, third person, includes what it does AND when to use it

## Documentation

- **[SKILL.md](./SKILL.md)** - Main skill documentation with core guidelines
- **[Best Practices](./SKILL_AUTHORING_BEST_PRACTICES.md)** - Expanded guide with detailed examples
- **[Structure Guide](./reference/structure.md)** - Progressive disclosure and file organization
- **[Patterns Reference](./reference/patterns.md)** - Common skill patterns with examples
- **[Advanced Topics](./reference/advanced.md)** - Error handling, scripts, and dependencies
- **[Validation Checklist](./reference/checklist.md)** - Pre-deployment quality checks

## Anti-Patterns to Avoid

- Including information Claude already knows
- Overly rigid instructions for open-ended tasks
- Assuming context without verifying
- Silent failures or vague error messages
- Excessive file nesting beyond one level

## Contributing

When improving this skill:
1. Follow the principles documented in `SKILL.md`
2. Run through the checklist in `reference/checklist.md`
3. Test with Haiku, Sonnet, and Opus models

## License

This project provides guidance for creating Claude Skills as part of the Claude ecosystem.
