# Common Patterns

## Template Pattern

Provide output format templates. Match strictness to requirements.

### Strict template (for APIs, data formats)

```markdown
## Report structure

ALWAYS use this exact template:

\`\`\`markdown
# [Analysis Title]

## Executive summary
[One-paragraph overview]

## Key findings
- Finding 1 with data
- Finding 2 with data

## Recommendations
1. Specific recommendation
2. Specific recommendation
\`\`\`
```

### Flexible template (for adaptation)

```markdown
## Report structure

Sensible default, adapt based on analysis:

\`\`\`markdown
# [Analysis Title]

## Executive summary
[Overview]

## Key findings
[Adapt sections to discoveries]

## Recommendations
[Tailor to context]
\`\`\`
```

## Examples Pattern

For output quality that depends on examples, provide input/output pairs:

```markdown
## Commit message format

**Example 1:**
Input: Added user authentication with JWT tokens
Output:
\`\`\`
feat(auth): implement JWT-based authentication

Add login endpoint and token validation middleware
\`\`\`

**Example 2:**
Input: Fixed bug where dates displayed incorrectly
Output:
\`\`\`
fix(reports): correct date formatting in timezone conversion

Use UTC timestamps consistently across report generation
\`\`\`

**Example 3:**
Input: Updated dependencies and refactored error handling
Output:
\`\`\`
chore: update dependencies and refactor error handling

- Upgrade lodash to 4.17.21
- Standardize error response format
\`\`\`

Follow: type(scope): brief description, then details.
```

## Workflow Pattern

Break complex tasks into clear steps with progress tracking.

### Without code (analysis tasks)

```markdown
## Research synthesis workflow

Copy and track progress:

\`\`\`
- [ ] Step 1: Read all source documents
- [ ] Step 2: Identify key themes
- [ ] Step 3: Cross-reference claims
- [ ] Step 4: Create structured summary
- [ ] Step 5: Verify citations
\`\`\`

**Step 1: Read all source documents**
Review each document in `sources/`. Note main arguments.

**Step 2: Identify key themes**
Find patterns across sources. Where do they agree/disagree?

**Step 3: Cross-reference claims**
Verify each major claim appears in source material.

**Step 4: Create structured summary**
Organize by theme with supporting evidence.

**Step 5: Verify citations**
Check every claim references correct source. If incomplete, return to Step 3.
```

### With code (executable tasks)

```markdown
## PDF form filling workflow

\`\`\`
- [ ] Step 1: Analyze form (run analyze_form.py)
- [ ] Step 2: Create field mapping (edit fields.json)
- [ ] Step 3: Validate mapping (run validate_fields.py)
- [ ] Step 4: Fill form (run fill_form.py)
- [ ] Step 5: Verify output (run verify_output.py)
\`\`\`

**Step 1: Analyze the form**
Run: `python scripts/analyze_form.py input.pdf`

**Step 2: Create field mapping**
Edit `fields.json` to add values.

**Step 3: Validate mapping**
Run: `python scripts/validate_fields.py fields.json`
Fix errors before continuing.

**Step 4: Fill the form**
Run: `python scripts/fill_form.py input.pdf fields.json output.pdf`

**Step 5: Verify output**
Run: `python scripts/verify_output.py output.pdf`
If fails, return to Step 2.
```

## Conditional Workflow Pattern

Guide through decision points:

```markdown
## Document modification workflow

1. Determine modification type:

   **Creating new content?** → Creation workflow below
   **Editing existing content?** → Editing workflow below

2. Creation workflow:
   - Use docx-js library
   - Build from scratch
   - Export to .docx

3. Editing workflow:
   - Unpack existing document
   - Modify XML directly
   - Validate after each change
   - Repack when complete
```

## Feedback Loop Pattern

Run validator → fix errors → repeat

### Without code

```markdown
## Content review process

1. Draft content following STYLE_GUIDE.md
2. Review against checklist:
   - Terminology consistency
   - Example format
   - Required sections present
3. If issues found:
   - Note each with section reference
   - Revise content
   - Review again
4. Only proceed when all requirements met
```

### With code

```markdown
## Document editing process

1. Make edits to `word/document.xml`
2. **Validate immediately**: `python scripts/validate.py unpacked_dir/`
3. If validation fails:
   - Review error message
   - Fix issues in XML
   - Run validation again
4. **Only proceed when validation passes**
5. Rebuild: `python scripts/pack.py unpacked_dir/ output.docx`
```

## Content Guidelines

### Avoid time-sensitive information

**Bad**:
```markdown
If before August 2025, use old API.
After August 2025, use new API.
```

**Good**:
```markdown
## Current method
Use v2 API: `api.example.com/v2/messages`

## Old patterns
<details>
<summary>Legacy v1 API (deprecated)</summary>
The v1 API used: `api.example.com/v1/messages`
No longer supported.
</details>
```

### Consistent terminology

Choose one term, use it throughout:
- Always "API endpoint" (not "URL", "route", "path")
- Always "field" (not "box", "element", "control")
- Always "extract" (not "pull", "get", "retrieve")
