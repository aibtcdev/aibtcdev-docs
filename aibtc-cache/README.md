# AIBTC Cache Services

The AIBTC Cache is a Cloudflare Workers-based caching layer that provides efficient access to blockchain data and other services. It helps reduce API rate limits, improve performance, and enhance reliability for applications in the AIBTC ecosystem.

## Environments

The cache service is available at the following URLs:

- **Production**: [https://cache.aibtc.dev](https://cache.aibtc.dev) (main branch)
- **Staging**: [https://cache-staging.aibtc.dev](https://cache-staging.aibtc.dev) (staging branch)
- **Preview**: Preview URLs are generated for each PR and change with each deployment (e.g., `https://aibtcdev-cache-preview.hosting-962.workers.dev/`)

## Key Components

- **Durable Objects**: Stateful components that handle specific API caching needs
- **Rate Limiting**: Intelligent rate limiting to prevent exceeding external API quotas
- **Caching**: KV-based caching with configurable TTLs
- **Request Queuing**: Orderly processing of requests with automatic retries
- **[Error Handling](error-handling.md)**: Standardized error responses with detailed information
- **Logging**: Comprehensive logging with performance tracking

## Available Services

The cache currently supports the following services:

- [Contract Calls](/aibtc-cache/contract-calls/README.md) - For interacting with Stacks smart contracts

## Architecture

The cache uses a multi-layered approach:

1. **Request Layer**: Handles incoming requests and routes them to appropriate Durable Objects
2. **Durable Object Layer**: Maintains state and handles service-specific logic
3. **Service Layer**: Provides reusable services for API interactions, caching, and rate limiting
4. **Utility Layer**: Common utilities for request/response handling and data transformation

## Response Format

All API responses follow a standardized format:

### Success Response

```json
{
  "success": true,
  "data": {
    // The actual response data
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

## Getting Started

To use the cache in your application, make requests to the appropriate endpoints. See the service-specific documentation for details on available endpoints and request formats.

### Example: Calling a read-only function

```javascript
// Example: Call get-proposal function
fetch(
  "https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal",
  {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      functionArgs: [
        {
          type: "uint",
          value: "3",
        },
      ],
    }),
  }
)
  .then((response) => response.json())
  .then((result) => {
    if (result.success) {
      console.log("Proposal data:", result.data);
    } else {
      console.error("Error:", result.error);
    }
  });
```

### Example: Fetching a contract ABI

```javascript
// Example: Fetch the ABI for media3-core-proposals-v2
fetch(
  "https://cache.aibtc.dev/contract-calls/abi/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-core-proposals-v2"
)
  .then((response) => response.json())
  .then((result) => {
    if (result.success) {
      console.log("Contract ABI:", result.data);
    } else {
      console.error("Error:", result.error);
    }
  });
```
