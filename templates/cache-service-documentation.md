---
description: Template for documenting cache services
---

# Cache Service Documentation Template

Use this template when documenting the high-level aspects of a cache service.

## High-Level Overview

```yaml
---
description: [One-line description of the service's purpose]
---
```

# [Service Name]

[1-2 paragraph introduction explaining what this service does and why it matters]

## Key Features

- **[Feature 1]**: [Brief explanation]
- **[Feature 2]**: [Brief explanation]
- **[Feature 3]**: [Brief explanation]

## Service Architecture

```mermaid
flowchart TD
    A[Client] -->|Request| B[Service Endpoint]
    B -->|Process| C[Cache Layer]
    C -->|Cache Miss| D[External API/Service]
    D -->|Response| C
    C -->|Cache Hit/Store| B
    B -->|Response| A
```

[Brief explanation of the architecture]

## Endpoints

| Endpoint               | Method        | Description         |
| ---------------------- | ------------- | ------------------- |
| `/[path]/[endpoint-1]` | [HTTP Method] | [Brief description] |
| `/[path]/[endpoint-2]` | [HTTP Method] | [Brief description] |

## Request/Response Format

### Success Response

```json
{
  "success": true,
  "data": {
    "key1": "value1",
    "key2": "value2"
  }
}
```

### Error Response

```json
{
  "success": false,
  "error": {
    "id": "unique-error-id",
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      // Optional additional error details
    }
  }
}
```

## Caching Behavior

- **Default TTL**: [Time in seconds]
- **Cache Key Generation**: [How cache keys are generated]
- **Cache Busting**: [How to force a fresh request]
- **Custom TTL**: [How to set a custom TTL]

## Performance Considerations

- **Rate Limiting**: [Description of rate limits]
- **Request Queuing**: [How requests are queued]
- **Timeout Handling**: [How timeouts are handled]
- **Retry Strategy**: [How retries are implemented]

## Related Services

- **[Related Service 1]**: [Brief description of relationship]
- **[Related Service 2]**: [Brief description of relationship]
