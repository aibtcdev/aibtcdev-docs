# Contract Calls API Design

The Contract Calls API provides a caching layer for interacting with Stacks smart contracts. This document provides a comprehensive overview of how the API works, its key features, and best practices for integration.

## Key Features

### Standardized Response Format

All endpoints return responses in a consistent format:

#### Success Response

```json
{
  "success": true,
  "data": {
    // The actual response data
  }
}
```

#### Error Response

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

### Caching

- Responses are cached to reduce API calls and improve performance
- Default TTL (Time-To-Live) is configurable per endpoint
- Cache control options provide fine-grained control:
  - `bustCache`: Bypass the cache and force a fresh request
  - `skipCache`: Don't cache the result of this specific request
  - `ttl`: Set a custom TTL for this specific request

### Rate Limiting

- Implements token bucket algorithm to prevent exceeding Stacks API rate limits
- Automatic queuing of requests when rate limits are approached
- Prioritization of requests to ensure fair processing

### Error Handling

- Standardized error codes across all endpoints
- Unique error IDs for easier debugging and tracking
- Detailed error messages and context in the response

### Validation

- Contract addresses are validated for correct format and network
- Function names are validated against contract ABIs
- Function arguments are validated for correct types and formats

## Architecture

The Contract Calls API uses a multi-layered approach:

1. **Request Layer**: Handles incoming requests and routes them to the Durable Object
2. **Durable Object Layer**: Maintains state for rate limiting and caching
3. **Service Layer**: Provides contract fetching, ABI validation, and other services
4. **Utility Layer**: Common utilities for request/response handling and data transformation

## Best Practices

### Handling Responses

Always check the `success` field to determine if the request was successful:

```javascript
const response = await fetch(
  "https://cache.aibtc.dev/contract-calls/read-only/..."
);
const result = await response.json();

if (result.success) {
  // Handle successful response
  const data = result.data;
  // Process data...
} else {
  // Handle error response
  const error = result.error;
  console.error(`Error ${error.code}: ${error.message}`);
  // Handle specific error codes...
}
```

### Error Handling

Implement specific handling for common error codes:

- `INVALID_CONTRACT_ADDRESS`: Validate contract addresses before sending
- `INVALID_FUNCTION`: Check function names against contract ABIs
- `INVALID_ARGUMENTS`: Ensure arguments match the expected types
- `UPSTREAM_API_ERROR`: Handle temporary Stacks API issues with retries

### Optimizing Cache Usage

- Use consistent cache keys for the same data
- Only use `bustCache` when you need the latest data
- Use `skipCache` for frequently changing data that shouldn't be cached
- Set custom `ttl` values based on how frequently the data changes
- Group related calls to minimize API requests

### Working with BigInt Values

For large numbers that exceed JavaScript's safe integer limits:

- Values are returned as strings with the `n` suffix
- Use BigInt in JavaScript to handle these values
- In other languages, parse them as appropriate numeric types

## Integration Examples

See the [Integration Examples](integration-examples.md) document for detailed code examples in various programming languages.
