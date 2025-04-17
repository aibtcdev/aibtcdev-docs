---
description: Template for documenting prompts for specific domains or tools
---

# Prompting Documentation Template

Use this template when documenting prompts to ensure consistency across all prompting guides.

## High-Level Overview

```yaml
---
description: [One-line description of the prompting guide's purpose]
---
```

## [Domain/Tool] Prompting Guide

[1-2 paragraph introduction explaining the purpose of these prompts and when to use them]

## Basic Operations

### [Operation 1]

```
[Example prompt with placeholders]
```

**Parameters**:

- `[param1]`: [description and format]
- `[param2]`: [description and format]

**Expected Output**: [Description of what to expect]

### [Operation 2]

```
[Example prompt with placeholders]
```

**Parameters**:

- `[param1]`: [description and format]
- `[param2]`: [description and format]

**Expected Output**: [Description of what to expect]

## Advanced Operations

### [Advanced Operation 1]

```
[Example prompt with placeholders]
```

**Parameters**:

- `[param1]`: [description and format]
- `[param2]`: [description and format]

**Expected Output**: [Description of what to expect]

## Complete Workflows

### [Workflow Name]

[Brief description of the workflow]

1. **[Step 1]**

   ```
   [Prompt for step 1]
   ```

2. **[Step 2]**

   ```
   [Prompt for step 2]
   ```

3. **[Step 3]**
   ```
   [Prompt for step 3]
   ```

**Notes**: [Any additional information about the workflow]

## Troubleshooting

### Common Issues

| Issue     | Solution     |
| --------- | ------------ |
| [Issue 1] | [Solution 1] |
| [Issue 2] | [Solution 2] |

## Related Resources

- **[Related Resource 1]**: [Brief description]
- **[Related Resource 2]**: [Brief description]

## Review Checklist

Before submitting documentation:

- [ ] Follows the appropriate template structure
- [ ] Includes all required sections
- [ ] Has exactly one H1 title
- [ ] YAML frontmatter is at the top with description
- [ ] Introduction follows immediately after title
- [ ] Heading levels are used correctly (H1 → H2 → H3)
- [ ] Prompt examples are complete and functional
- [ ] Parameters are clearly documented
- [ ] Expected outputs are described
- [ ] Workflows are documented with step-by-step instructions
- [ ] No spelling or grammatical errors
- [ ] Technical accuracy has been verified
- [ ] Examples use realistic values
- [ ] Troubleshooting section addresses common issues
- [ ] Content is accessible to the target audience

## Versioning and Updates

- Note when documentation was last updated
- Indicate which version of the tools/services the prompts apply to
- Highlight significant changes from previous versions
- Maintain backward compatibility information where relevant
