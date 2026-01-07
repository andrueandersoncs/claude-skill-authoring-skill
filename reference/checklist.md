# Skill Validation Checklist

Use this checklist before sharing a skill.

## Core Quality

- [ ] **Description is specific** with key terms for discovery
- [ ] **Description includes both** what the skill does AND when to use it
- [ ] **Description in third person** ("Processes files" not "I can process")
- [ ] **SKILL.md body under 500 lines**
- [ ] **Additional details in separate files** (if needed)
- [ ] **No time-sensitive information** (or in "old patterns" section)
- [ ] **Consistent terminology** throughout
- [ ] **Examples are concrete**, not abstract
- [ ] **File references one level deep** from SKILL.md
- [ ] **Progressive disclosure** used appropriately
- [ ] **Workflows have clear steps** with checklists for complex tasks

## Frontmatter

- [ ] **name**: Max 64 chars, lowercase/numbers/hyphens only
- [ ] **name**: No reserved words ("anthropic", "claude")
- [ ] **description**: Non-empty, max 1024 chars
- [ ] **description**: No XML tags

## Code and Scripts

- [ ] **Scripts solve problems** rather than punt to Claude
- [ ] **Error handling explicit** and helpful
- [ ] **No "voodoo constants"** (all values justified)
- [ ] **Required packages listed** and verified as available
- [ ] **Scripts have clear documentation**
- [ ] **No Windows-style paths** (all forward slashes)
- [ ] **Validation/verification steps** for critical operations
- [ ] **Feedback loops** for quality-critical tasks

## Testing

- [ ] **At least three evaluations** created
- [ ] **Tested with Haiku** - does it provide enough guidance?
- [ ] **Tested with Sonnet** - is it clear and efficient?
- [ ] **Tested with Opus** - does it avoid over-explaining?
- [ ] **Tested with real usage scenarios**
- [ ] **Team feedback incorporated** (if applicable)

## Evaluation-Driven Development

1. **Identify gaps**: Run Claude on tasks without skill, document failures
2. **Create evaluations**: Build 3+ scenarios testing these gaps
3. **Establish baseline**: Measure performance without skill
4. **Write minimal instructions**: Just enough to pass evaluations
5. **Iterate**: Execute evaluations, compare baseline, refine

## Iterative Development Process

### Creating new skills

1. Complete task with Claude, noting context you provide
2. Identify reusable pattern
3. Ask Claude to create skill capturing the pattern
4. Review for conciseness (remove what Claude already knows)
5. Improve information architecture
6. Test with fresh Claude instance
7. Iterate based on observed behavior

### Improving existing skills

1. Use skill in real workflows
2. Observe behavior: struggles, successes, unexpected choices
3. Return to Claude with current SKILL.md and observations
4. Review suggestions (prominence, language strength, structure)
5. Apply changes and test again
6. Repeat based on usage

## Observation Checklist

Watch for these when testing:

- [ ] **Unexpected exploration paths** - structure may not be intuitive
- [ ] **Missed connections** - links may need to be more explicit
- [ ] **Overreliance on sections** - content may belong in SKILL.md
- [ ] **Ignored content** - file may be unnecessary or poorly signaled
- [ ] **Skill triggers correctly** - name/description enable discovery

## Evaluation Example Format

```json
{
  "skills": ["pdf-processing"],
  "query": "Extract all text from this PDF and save to output.txt",
  "files": ["test-files/document.pdf"],
  "expected_behavior": [
    "Successfully reads PDF using appropriate library",
    "Extracts text from all pages",
    "Saves extracted text to output.txt"
  ]
}
```
