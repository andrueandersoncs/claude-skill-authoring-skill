# Advanced: Skills with Executable Code

## Solve, Don't Punt

Handle errors in scripts rather than punting to Claude.

### Good: Handle explicitly

```python
def process_file(path):
    """Process file, creating if it doesn't exist."""
    try:
        with open(path) as f:
            return f.read()
    except FileNotFoundError:
        print(f"File {path} not found, creating default")
        with open(path, 'w') as f:
            f.write('')
        return ''
    except PermissionError:
        print(f"Cannot access {path}, using default")
        return ''
```

### Bad: Punt to Claude

```python
def process_file(path):
    return open(path).read()  # Just fails
```

## Document Constants

Avoid "voodoo constants" - justify all values.

### Good: Self-documenting

```python
# HTTP requests typically complete within 30 seconds
# Longer timeout accounts for slow connections
REQUEST_TIMEOUT = 30

# Three retries balances reliability vs speed
# Most intermittent failures resolve by second retry
MAX_RETRIES = 3
```

### Bad: Magic numbers

```python
TIMEOUT = 47  # Why 47?
RETRIES = 5   # Why 5?
```

## Utility Scripts

Pre-made scripts are more reliable than generated code and save tokens.

### Script documentation format

```markdown
## Utility scripts

**analyze_form.py**: Extract form fields from PDF
\`\`\`bash
python scripts/analyze_form.py input.pdf > fields.json
\`\`\`

Output:
\`\`\`json
{
  "field_name": {"type": "text", "x": 100, "y": 200},
  "signature": {"type": "sig", "x": 150, "y": 500}
}
\`\`\`

**validate_boxes.py**: Check for overlapping bounding boxes
\`\`\`bash
python scripts/validate_boxes.py fields.json
# Returns: "OK" or lists conflicts
\`\`\`
```

### Execution vs reference

Make intent clear:
- **Execute**: "Run `analyze_form.py` to extract fields"
- **Reference**: "See `analyze_form.py` for the extraction algorithm"

Prefer execution - more reliable, efficient.

## Visual Analysis

When inputs can be rendered, have Claude analyze images:

```markdown
## Form layout analysis

1. Convert PDF to images:
   \`\`\`bash
   python scripts/pdf_to_images.py form.pdf
   \`\`\`

2. Analyze each page image to identify form fields
3. Claude can see field locations visually
```

## Verifiable Intermediate Outputs

For complex tasks, create plan files that get validated before execution.

### The problem

Asking Claude to update 50 form fields might result in:
- References to non-existent fields
- Conflicting values
- Missed required fields

### The solution

Add intermediate `changes.json` validated before applying:

```
analyze → create plan file → validate plan → execute → verify
```

### Implementation

Make validation verbose with specific errors:

```
"Field 'signature_date' not found. Available fields: customer_name, order_total, signature_date_signed"
```

### When to use

- Batch operations
- Destructive changes
- Complex validation rules
- High-stakes operations

## Package Dependencies

### Platform limitations

- **claude.ai**: Can install from npm, PyPI, pull from GitHub
- **Anthropic API**: No network access, no runtime installation

### Documentation

List required packages and verify availability:

```markdown
## Dependencies

Install required packages:
\`\`\`bash
pip install pypdf pdfplumber
\`\`\`

Then use:
\`\`\`python
from pypdf import PdfReader
import pdfplumber
\`\`\`
```

## MCP Tool References

Use fully qualified names to avoid "tool not found" errors.

**Format**: `ServerName:tool_name`

```markdown
Use the BigQuery:bigquery_schema tool for table schemas.
Use the GitHub:create_issue tool for issues.
```

Without server prefix, Claude may fail to locate tools when multiple MCP servers are available.

## Runtime Environment

### How Claude accesses skills

1. **Metadata pre-loaded**: name/description loaded at startup
2. **Files read on-demand**: Claude reads SKILL.md and other files when needed
3. **Scripts executed efficiently**: Output consumes tokens, not source code
4. **No context penalty**: Large files don't consume tokens until read

### Authoring implications

- File paths matter (use forward slashes)
- Name files descriptively (`form_validation_rules.md` not `doc2.md`)
- Organize directories by domain or feature
- Bundle comprehensive resources freely
- Prefer scripts for deterministic operations
- Test file access patterns with real requests
