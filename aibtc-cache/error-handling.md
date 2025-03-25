# Error Handling

The AIBTC Cache uses a standardized approach to error handling across all services. This document explains the error structure, common error codes, and best practices for handling errors.

## Error Response Structure

All error responses follow this format:

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

### Fields

- **id**: A unique identifier for this specific error instance. Useful for tracking in logs and debugging.
- **code**: A standardized error code from the `ErrorCode` enum.
- **message**: A human-readable description of what went wrong.
- **details**: Additional context-specific information about the error.

## Common Error Codes

### General Errors

- **INTERNAL_ERROR**: An unexpected internal error occurred.
- **NOT_FOUND**: The requested resource was not found.
- **INVALID_REQUEST**: The request was malformed or invalid.
- **UNAUTHORIZED**: The request lacks valid authentication.

### API Specific Errors

- **RATE_LIMIT_EXCEEDED**: The API rate limit has been exceeded.
- **UPSTREAM_API_ERROR**: An error occurred in an upstream API (e.g., Stacks API).

### Validation Errors

- **VALIDATION_ERROR**: General validation error.
- **INVALID_CONTRACT_ADDRESS**: The contract address is invalid.
- **INVALID_FUNCTION**: The function doesn't exist in the contract.
- **INVALID_ARGUMENTS**: The arguments don't match what the function expects.

### Cache Errors

- **CACHE_ERROR**: An error occurred with the caching system.

### Configuration Errors

- **CONFIG_ERROR**: An error in the configuration.

## Error Handling Best Practices

### Client-Side Error Handling

```javascript
async function callContract(contractAddress, contractName, functionName, args) {
  try {
    const response = await fetch(
      `https://cache.aibtc.dev/contract-calls/read-only/${contractAddress}/${contractName}/${functionName}`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          functionArgs: args
        })
      }
    );
    
    const result = await response.json();
    
    if (result.success) {
      return result.data;
    } else {
      // Handle specific error codes
      switch (result.error.code) {
        case 'INVALID_CONTRACT_ADDRESS':
          console.error('The contract address is invalid:', result.error.details.address);
          break;
        case 'INVALID_FUNCTION':
          console.error(`Function ${result.error.details.function} not found in contract`);
          break;
        case 'INVALID_ARGUMENTS':
          console.error(`Invalid arguments: ${result.error.details.reason}`);
          break;
        case 'UPSTREAM_API_ERROR':
          console.error('Error from Stacks API:', result.error.message);
          // This might be a temporary issue, could implement retry logic
          break;
        case 'RATE_LIMIT_EXCEEDED':
          console.error('Rate limit exceeded, try again later');
          // Implement backoff strategy
          break;
        default:
          console.error(`Error: ${result.error.code} - ${result.error.message}`);
      }
      
      throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
    }
  } catch (error) {
    // Handle network errors or other exceptions
    console.error('Failed to call contract:', error);
    throw error;
  }
}
```

### Retry Strategies

For certain error types, implementing a retry strategy can improve reliability:

```javascript
async function fetchWithRetry(url, options, maxRetries = 3, initialDelay = 1000) {
  let retries = 0;
  let delay = initialDelay;
  
  while (true) {
    try {
      const response = await fetch(url, options);
      const result = await response.json();
      
      if (result.success) {
        return result.data;
      }
      
      // Only retry certain error types
      if (['UPSTREAM_API_ERROR', 'RATE_LIMIT_EXCEEDED'].includes(result.error.code) && retries < maxRetries) {
        retries++;
        console.log(`Retrying after error: ${result.error.code} (attempt ${retries}/${maxRetries})`);
        await new Promise(resolve => setTimeout(resolve, delay));
        delay *= 2; // Exponential backoff
        continue;
      }
      
      throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
    } catch (error) {
      if (retries < maxRetries) {
        retries++;
        console.log(`Retrying after exception (attempt ${retries}/${maxRetries})`);
        await new Promise(resolve => setTimeout(resolve, delay));
        delay *= 2; // Exponential backoff
        continue;
      }
      throw error;
    }
  }
}
```

## Error Logging

When handling errors, it's useful to log the error ID for later reference:

```javascript
try {
  const result = await callContract(...);
  // Process result
} catch (error) {
  if (error.errorId) {
    console.error(`Error occurred with ID ${error.errorId}. Please reference this ID when reporting issues.`);
  }
  // Handle error
}
```

## Common Error Scenarios and Solutions

| Error Code | Common Cause | Solution |
|------------|--------------|----------|
| `INVALID_CONTRACT_ADDRESS` | Typo in contract address | Double-check the contract address format and network prefix |
| `INVALID_FUNCTION` | Function name doesn't exist in contract | Verify the function name against the contract ABI |
| `INVALID_ARGUMENTS` | Wrong argument types or count | Check the contract ABI for the expected argument types |
| `UPSTREAM_API_ERROR` | Stacks API is down or returning errors | Implement retry logic with exponential backoff |
| `RATE_LIMIT_EXCEEDED` | Too many requests in a short period | Add rate limiting on your side or implement backoff |
