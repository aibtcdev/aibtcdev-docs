---
description: Style guide for documentation templates
---

# Documentation Template Style Guide

This style guide provides guidelines for maintaining consistency, readability, and best practices when creating or updating documentation using our templates.

## General Principles

- **Consistency**: Follow established patterns across all documentation
- **Clarity**: Write for understanding, not to impress
- **Completeness**: Include all necessary information without redundancy
- **Accessibility**: Make documentation approachable for all skill levels
- **Maintainability**: Structure content to be easily updated

## Structure and Organization

### Document Structure

1. **YAML Frontmatter**: Always include a description at the top
   ```yaml
   ---
   description: Concise one-line description of the document's purpose
   ---
   ```

2. **Title and Introduction**: Start with a clear title (H1) and 1-2 paragraph introduction
   - Title should match the document's purpose
   - Introduction should explain what, why, and for whom

3. **Key Features**: List 3-5 most important features with brief explanations
   - Use bold for feature names
   - Keep explanations to one line each

4. **Visual Diagrams**: Include Mermaid diagrams for complex workflows
   - Keep diagrams focused on key interactions
   - Include a brief explanation below the diagram

5. **Details Section**: Organize detailed information in logical sections
   - Use consistent heading levels (H2 for major sections, H3 for subsections)
   - Group related information together

6. **Examples**: Provide practical, real-world examples
   - Include complete code snippets that can be copied and used
   - Explain what the example demonstrates

7. **Related Resources**: End with links to related documentation
   - Briefly explain the relationship to the current document

### Tables

- Use tables for structured information (parameters, errors, etc.)
- Include clear column headers
- Align column content consistently
- Sort rows logically (alphabetically, by importance, etc.)

## Writing Style

### Language

- Use active voice: "The function returns a value" not "A value is returned by the function"
- Write in present tense: "The tool creates" not "The tool will create"
- Address the reader directly: "You can configure" or use imperative: "Configure the settings"
- Be concise: Eliminate unnecessary words and phrases
- Use simple language: Avoid jargon unless necessary and defined

### Code Examples

- Include language identifier in code blocks
- Use realistic values in examples
- Comment complex or non-obvious code
- Format code according to language conventions
- Ensure examples are complete and functional

### Formatting

- Use **bold** for emphasis and UI elements
- Use `code formatting` for:
  - Function names
  - Parameter names
  - File paths
  - Code snippets
  - Terminal commands
- Use blockquotes for notes or important callouts
- Use numbered lists for sequential steps
- Use bullet lists for non-sequential items

## Template-Specific Guidelines

### Smart Contract Documentation

- Include contract address format and naming conventions
- Document all public and read-only functions
- List all error codes with explanations
- Provide complete function call examples
- Include security considerations specific to the contract

### Cache Service Documentation

- Document caching behavior (TTL, invalidation, etc.)
- Include rate limiting information
- Provide examples with error handling
- Document all request parameters and response formats
- Include performance considerations

### Agent Tool Documentation

- Focus on how agents should use the tool
- Include example prompts that work with the tool
- Document all input parameters and expected outputs
- Provide complete workflow examples
- Include troubleshooting information

### Prompting Documentation

- Use realistic, complete prompt examples
- Explain all placeholders and variables
- Include expected outputs
- Provide troubleshooting for common issues
- Show complete workflows with multiple prompts

## Automation Considerations

When updating documentation for automation:

- Use consistent parameter naming across related documents
- Include machine-readable sections where appropriate
- Maintain consistent structure for easier parsing
- Use predictable patterns for code examples
- Keep formatting simple and standard

## Review Checklist

Before submitting documentation:

- [ ] Follows the appropriate template structure
- [ ] Includes all required sections
- [ ] Code examples are complete and functional
- [ ] Links to related documentation are correct
- [ ] No spelling or grammatical errors
- [ ] Formatting is consistent
- [ ] Technical accuracy has been verified
- [ ] Examples use realistic values
- [ ] Security considerations are addressed
- [ ] Content is accessible to the target audience

## Versioning and Updates

- Note when documentation was last updated
- Indicate which version of software/contracts the documentation applies to
- Highlight significant changes from previous versions
- Maintain backward compatibility information where relevant
