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

## Document Structure Standards

### Required Elements

1. **YAML Frontmatter**: Always include at the very top of every document
   ```yaml
   ---
   description: Concise one-line description of the document's purpose
   ---
   ```

2. **Title (H1)**: Every document must have exactly one H1 title
   - Must be the first content after the frontmatter
   - Should clearly describe the document's purpose

3. **Introduction**: 1-2 paragraphs immediately following the title
   - Explain what the document covers and why it matters
   - Identify the target audience

4. **Heading Hierarchy**:
   - **H1 (#)**: Document title only (only one per document)
   - **H2 (##)**: Major sections
   - **H3 (###)**: Subsections
   - **H4 (####)**: Minor subsections (use sparingly)

### Standard Sections

Most documentation should include these sections in this order:

1. **Key Features**: List 3-5 most important features with brief explanations
   - Use bold for feature names
   - Keep explanations to one line each

2. **Overview Table**: When applicable, provide a summary table of components
   - Use consistent column headers across similar documents
   - Align text left, numbers center

3. **Visual Diagrams**: Include Mermaid diagrams for complex workflows
   - Keep diagrams focused on key interactions
   - Always include an explanation paragraph below each diagram
   - Different diagram types are acceptable based on content needs

4. **Details Section**: Organize detailed information in logical sections
   - Use consistent heading levels (H2 for major sections, H3 for subsections)
   - Group related information together

5. **Examples**: Provide practical, real-world examples
   - Include complete code snippets that can be copied and used
   - Explain what the example demonstrates
   - Use consistent formatting within code blocks

6. **Error Handling/Troubleshooting**: Document common errors and solutions
   - Use tables for error codes and resolutions
   - Include practical troubleshooting steps

7. **Related Resources**: End with links to related documentation
   - Briefly explain the relationship to the current document

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

## Table Formatting Standards

- Every table must have headers
- Use consistent column headers across similar tables
- Left-align text columns
- Center-align numeric columns
- Use title case for column headers
- Sort rows logically (alphabetically, by importance, etc.)
- Keep table width reasonable (avoid too many columns)

## Mermaid Diagram Standards

- Choose appropriate diagram type for the content:
  - Flowchart: For processes and decision trees
  - Sequence: For API interactions and time-based flows
  - Class: For object relationships
- Include clear labels for all components
- Use consistent naming conventions
- Add a paragraph explanation after every diagram
- Keep diagrams focused on key interactions (avoid excessive detail)

## Review Checklist

Before submitting documentation:

- [ ] Follows the appropriate template structure
- [ ] Includes all required sections
- [ ] Has exactly one H1 title
- [ ] YAML frontmatter is at the top with description
- [ ] Introduction follows immediately after title
- [ ] Heading levels are used correctly (H1 → H2 → H3)
- [ ] Code examples are complete and functional
- [ ] Tables have clear headers and consistent formatting
- [ ] Mermaid diagrams have explanations
- [ ] Links to related documentation are correct
- [ ] No spelling or grammatical errors
- [ ] Technical accuracy has been verified
- [ ] Examples use realistic values
- [ ] Security considerations are addressed
- [ ] Content is accessible to the target audience

## Versioning and Updates

- Note when documentation was last updated
- Indicate which version of software/contracts the documentation applies to
- Highlight significant changes from previous versions
- Maintain backward compatibility information where relevant
