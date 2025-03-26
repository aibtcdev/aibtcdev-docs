# Contract Calls Endpoints

The Contract Calls Durable Object provides a caching layer for interacting with Stacks smart contracts. It allows you to make read-only function calls to any Stacks smart contract while benefiting from caching, rate limiting, and automatic retries.

## Features

- **Caching**: Responses are cached to reduce API calls and improve performance
- **Rate Limiting**: Prevents exceeding Stacks API rate limits
- **Automatic Retries**: Failed requests are automatically retried with exponential backoff
- **Validation**: Contract addresses, functions, and arguments are validated before execution
- **Standardized Responses**: All responses follow a consistent format with success/error handling
- **Error Tracking**: Unique error IDs for easier debugging and tracking

## Base Path

All contract call endpoints are available under:
```
/contract-calls
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| [API Overview](overview.md) | Comprehensive overview of the API architecture and features |
| [Read-Only Function Calls](read-only-calls.md) | Make read-only calls to smart contract functions |
| [Contract ABI](contract-abi.md) | Retrieve the ABI for a smart contract |
| [Known Contracts](known-contracts.md) | List all contracts accessed through the cache |
| [Decode Clarity Value](decode-clarity-value.md) | Decode Clarity values into JavaScript/JSON |
| [Clarity Value Types](clarity-value-types.md) | Reference for Clarity value types |
| [Integration Examples](integration-examples.md) | Examples for frontend and backend integration |

## Response Format

All endpoints return responses in a standardized format:

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
