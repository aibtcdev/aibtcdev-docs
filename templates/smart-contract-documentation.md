---
description: Template for documenting smart contracts
---

# Smart Contract Documentation Template

Use this template when documenting smart contracts to ensure consistency across all contract documentation.

## High-Level Overview

```yaml
---
description: [One-line description of the contract's purpose]
---
```

# [Contract Name]

[1-2 paragraph introduction explaining what the contract does and why it matters]

## Key Features

- **[Feature 1]**: [Brief explanation]
- **[Feature 2]**: [Brief explanation]
- **[Feature 3]**: [Brief explanation]

## Quick Reference

| Property       | Value                           |
| -------------- | ------------------------------- |
| Contract Name  | `[contract-name]`               |
| Version        | [version number]                |
| Implements     | [traits implemented]            |
| Key Parameters | [important configurable values] |

## How It Works

```mermaid
flowchart TD
    A["Actor 1"]
    B["Contract"]
    C["Actor 2"]
    D["Outcome 1"]
    E["Outcome 2"]
    
    subgraph Contract Functions
        BA["Function 1"]
        BB["Function 2"]
    end
    
    A -->|"Action"| B
    C -->|"Action"| B
    B --> BA
    B --> BB
    BA -->|"Result 1"| D
    BB -->|"Result 2"| E
```

[Brief explanation of the workflow]

## Public Functions

### `[function-name]`

**Purpose**: [What this function does]

**Parameters**:

- `[param1]`: [type] - [description]
- `[param2]`: [type] - [description]

**Returns**: [return type] - [description]

**Example**:

```clarity
(contract-call? .[contract-name] [function-name] [example-params])
```

[Additional notes about usage, security considerations, etc.]

## Read-Only Functions

### `[function-name]`

**Purpose**: [What this function does]

**Parameters**:

- `[param1]`: [type] - [description]
- `[param2]`: [type] - [description]

**Returns**: [return type] - [description]

**Example**:

```clarity
(contract-call? .[contract-name] [function-name] [example-params])
```

## Print Events

| Event          | Description                | Data                         |
| -------------- | -------------------------- | ---------------------------- |
| `[event-name]` | [What triggers this event] | [Data included in the event] |

## Integration Examples

### [Example Use Case 1]

```clarity
;; Example of how to use this contract for a specific purpose
(contract-call? .[contract-name] [function-name] [params])
```

### [Example Use Case 2]

```clarity
;; Another example showing a different use case
(contract-call? .[contract-name] [function-name] [different-params])
```

## Error Handling

| Error Code | Constant     | Description              | Resolution                |
| ---------- | ------------ | ------------------------ | ------------------------- |
| u[code]    | [ERROR_NAME] | [What causes this error] | [How to resolve or avoid] |

## Security Considerations

- **[Security Feature 1]**: [Explanation]
- **[Security Feature 2]**: [Explanation]
- **[Security Risk 1]**: [Explanation and mitigation]

## Related Contracts

- **[Related Contract 1]**: [Brief description of relationship]
- **[Related Contract 2]**: [Brief description of relationship]
