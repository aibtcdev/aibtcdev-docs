# Utilities

The AIBTC Cache system includes several utility modules that provide common functionality used across the caching services.

## Request/Response Utilities

The `requests-responses-util.ts` module provides utilities for handling HTTP requests and responses.

### Functions

#### `corsHeaders(origin?: string): HeadersInit`

Creates CORS headers for cross-origin requests.

**Parameters:**

- `origin` (optional): Origin to allow, defaults to '\*' (all origins)

**Returns:** HeadersInit object with CORS headers

#### `createSuccessResponse<T>(data: T, status = 200): Response`

Creates a standardized success response with the data wrapped in a success object.

**Parameters:**

- `data`: The response data to include
- `status`: HTTP status code, defaults to 200

**Returns:** Response object with standardized format: `{ success: true, data: ... }`

#### `createErrorResponse(error: unknown): Response`

Creates a standardized error response.

**Parameters:**

- `error`: The error to include (ApiError or any other error)
- **Returns:** Response object with standardized format: `{ success: false, error: { id, code, message, details } }`

#### `createJsonResponse(body: unknown, status = 200): Response`

**Deprecated:** Use `createSuccessResponse` or `createErrorResponse` instead.

Creates a JSON response with appropriate headers.

**Parameters:**

- `body`: The response body (will be stringified if not already a string)
- `status`: HTTP status code, defaults to 200

**Returns:** Response object with JSON content type and CORS headers

#### `stringifyWithBigInt(value: unknown, replacer?: Function, space?: string | number): string`

Stringifies a value with special handling for BigInt values.

**Parameters:**

- `value`: The value to stringify
- `replacer` (optional): Replacer function for JSON.stringify
- `space` (optional): Space parameter for JSON.stringify formatting

**Returns:** JSON string with BigInt values converted to strings with 'n' suffix

#### `handleRequest<T>(handler: () => Promise<T>, env?: Env, options?: { slowThreshold?: number }): Promise<Response>`

Wraps a request handler function with standardized error handling and performance tracking.

**Parameters:**

- `handler`: The async function that handles the request
- `env` (optional): The environment for logging
- `options` (optional): Configuration options
  - `slowThreshold` (optional): Time in ms after which a request is considered slow (defaults to 1000ms)

**Returns:** A standardized Response object

**Example:**

```typescript
// Example of using handleRequest in a Cloudflare Worker
export async function handleReadOnlyCall(
  request: Request,
  env: Env
): Promise<Response> {
  return handleRequest(
    async () => {
      // Parse request body
      const body = await request.json();

      // Process the request
      const result = await processRequest(body);

      // Return the result (will be wrapped in a success response)
      return result;
    },
    env,
    { slowThreshold: 2000 } // Consider requests slow if they take more than 2 seconds
  );
}
```

**Benefits:**

- Automatically handles errors and converts them to standardized error responses
- Tracks request duration and logs slow requests
- Provides consistent request ID tracking for debugging
- Ensures all responses follow the standardized format

## Clarity Response Utilities

The `clarity-responses-util.ts` module provides utilities for working with Clarity values.

### Types

#### `SimplifiedClarityValue`

Interface for simplified Clarity value representation, used for non-TypeScript clients to easily construct Clarity values.

```typescript
interface SimplifiedClarityValue {
  type: string;
  value: any;
}
```

### Functions

#### `decodeClarityValues(value: ClarityValue, strictJsonCompat = false, preserveContainers = false): any`

Recursively decodes Clarity values into JavaScript objects.

**Parameters:**

- `value`: The Clarity value to decode
- `strictJsonCompat`: If true, ensures values are JSON compatible
- `preserveContainers`: If true, preserves container types in the output

**Returns:** JavaScript representation of the Clarity value

**Example with preserveContainers=false (default):**

```javascript
// Input: ResponseOkCV with UIntCV(123)
const clarityValue = responseOkCV(uintCV(123));

// Output: 123 (unwrapped value)
const decoded = decodeClarityValues(clarityValue);
```

**Example with preserveContainers=true:**

```javascript
// Input: ResponseOkCV with UIntCV(123)
const clarityValue = responseOkCV(uintCV(123));

// Output: { type: 'responseOk', value: 123 }
const decoded = decodeClarityValues(clarityValue, false, true);
```

#### `decodeTupleRecursively(tuple: TupleCV, strictJsonCompat = false, preserveContainers = false): any`

Recursively decodes a Clarity tuple into a JavaScript object.

**Parameters:**

- `tuple`: The Clarity tuple to decode
- `strictJsonCompat`: If true, ensures values are JSON compatible
- `preserveContainers`: If true, preserves container types in the output

**Returns:** JavaScript object representation of the tuple

#### `decodeListRecursively(list: ListCV, strictJsonCompat = false, preserveContainers = false): any[]`

Recursively decodes a Clarity list into a JavaScript array.

**Parameters:**

- `list`: The Clarity list to decode
- `strictJsonCompat`: If true, ensures values are JSON compatible
- `preserveContainers`: If true, preserves container types in the output

**Returns:** JavaScript array representation of the list

#### `convertToClarityValue(arg: ClarityValue | SimplifiedClarityValue): ClarityValue`

Converts a simplified Clarity value representation to a proper ClarityValue object.
This allows non-TypeScript clients to use a simpler JSON format for contract calls.

**Parameters:**

- `arg`: Either a ClarityValue object or a simplified representation

**Returns:** A proper ClarityValue object

**Throws:** ApiError with ErrorCode.VALIDATION_ERROR if the type is unsupported or the conversion fails

**Example:**

```javascript
// Convert a simplified representation to a ClarityValue
const simplifiedValue = {
  type: "tuple",
  value: {
    name: { type: "string", value: "Example" },
    amount: { type: "uint", value: "100" },
  },
};

// Result is equivalent to:
// tupleCV({
//   name: stringAsciiCV("Example"),
//   amount: uintCV(100)
// })
const clarityValue = convertToClarityValue(simplifiedValue);
```

## Timeout Utility

The `timeout-util.ts` module provides utilities for handling timeouts in asynchronous operations.

### Functions

#### `withTimeout<T>(promise: Promise<T>, timeoutMs: number, message?: string): Promise<T>`

Wraps a promise with a timeout, rejecting if the operation takes too long.

**Parameters:**

- `promise`: The promise to wrap with a timeout
- `timeoutMs`: Timeout in milliseconds
- `message`: Optional custom error message

**Returns:** A promise that resolves with the original promise's result or rejects with a timeout error

**Example:**

```typescript
import { withTimeout } from '../utils/timeout-util';

// Wrap an API call with a 5-second timeout
try {
  const result = await withTimeout(
    fetch('https://api.example.com/data'),
    5000,
    'API call timed out after 5 seconds'
  );
  // Process result
} catch (error) {
  if (error.message.includes('timed out')) {
    console.error('The operation timed out');
  } else {
    console.error('Operation failed:', error);
  }
}
```

## Stacks Network Utilities

The `stacks-network-util.ts` module provides utilities for working with Stacks networks.

### Functions

#### `getNetworkByPrincipal(principal: string): StacksNetworkName`

Determines the Stacks network (mainnet or testnet) based on a principal address.

Stacks addresses use different prefixes to indicate the network:

- SP/SM: Mainnet addresses
- ST/SN: Testnet addresses

**Parameters:**

- `principal`: A Stacks principal address

**Returns:** The network name ('mainnet' or 'testnet')

## Error Handling Utilities

The `api-error.ts` module provides standardized error handling across the application.

### Classes

#### `ApiError`

Standard API error class used throughout the application.

**Properties:**

- `code`: Error code from the ErrorCode enum
- `status`: HTTP status code
- `details`: Optional details to include in the error message
- `id`: Unique error ID for tracking

**Methods:**

- `constructor(code: ErrorCode, details?: Record<string, any>, id?: string)`: Create a new API error

### Enums

#### `ErrorCode`

Standardized error codes used throughout the application:

- General errors: `INTERNAL_ERROR`, `NOT_FOUND`, `INVALID_REQUEST`, `UNAUTHORIZED`
- API specific errors: `RATE_LIMIT_EXCEEDED`, `UPSTREAM_API_ERROR`
- Validation errors: `VALIDATION_ERROR`, `INVALID_CONTRACT_ADDRESS`, `INVALID_FUNCTION`, `INVALID_ARGUMENTS`
- Cache errors: `CACHE_ERROR`
- Configuration errors: `CONFIG_ERROR`

## Logging Utilities

The `logger-util.ts` module provides comprehensive logging capabilities across the application.

### Classes

#### `Logger`

A singleton logger that writes to console and optionally to KV storage for persistence.

**Properties:**

- `private static instance`: The singleton instance of the logger
- `private env?`: Optional Cloudflare Worker environment for KV storage
- `private readonly LOG_KEY_PREFIX`: Prefix for log keys in KV storage
- `private readonly MAX_LOG_AGE`: Maximum age of logs in KV storage (7 days by default)

**Methods:**

- `getInstance(env?: Env): Logger`: Get the singleton logger instance

  - `env` (optional): The Cloudflare Worker environment
  - Returns: The Logger instance

- `log(level: LogLevel, message: string, context?: Record<string, any>, error?: Error, duration?: number): string`: Log a message at the specified level

  - `level`: The log level (DEBUG, INFO, WARN, ERROR)
  - `message`: The log message
  - `context` (optional): Additional context data
  - `error` (optional): Error object if applicable
  - `duration` (optional): Duration of the operation in milliseconds
  - Returns: A unique log ID for tracking

- `debug(message: string, context?: Record<string, any>, duration?: number): string`: Log a debug message
- `info(message: string, context?: Record<string, any>, duration?: number): string`: Log an info message
- `warn(message: string, context?: Record<string, any>, duration?: number): string`: Log a warning message
- `error(message: string, error?: Error, context?: Record<string, any>, duration?: number): string`: Log an error message

**Private Methods:**

- `private generateId(): string`: Generates a unique ID for each log entry
- `private logToConsole(entry: LogEntry): void`: Logs to the console with appropriate formatting
- `private async logToKV(entry: LogEntry): Promise<void>`: Logs to KV storage for persistence (only for WARN and ERROR levels)

**Example:**

```typescript
// Get the logger instance
const logger = Logger.getInstance(env);

// Log at different levels
logger.debug("Processing request", { requestId: "123" });
logger.info("Request completed", { requestId: "123", duration: 150 });
logger.warn("Rate limit approaching", { requestsRemaining: 10 });

try {
  // Some operation that might fail
  throw new Error("Something went wrong");
} catch (error) {
  // Log the error with the error object
  logger.error("Failed to process request", error, { requestId: "123" });
}

// Log with duration tracking
const startTime = Date.now();
// ... perform operation
const duration = Date.now() - startTime;
logger.info("Operation completed", { result: "success" }, duration);
```

### Interfaces

#### `LogEntry`

Interface for structured log entries.

**Properties:**

- `id`: Unique identifier for the log entry
- `timestamp`: ISO timestamp of when the log was created
- `level`: The log level (DEBUG, INFO, WARN, ERROR)
- `message`: The log message
- `context?`: Optional additional context data
- `error?`: Optional error information
- `duration?`: Optional duration of the operation in milliseconds

### Enums

#### `LogLevel`

Log levels in order of increasing severity:

- `DEBUG`: Detailed information for debugging purposes
- `INFO`: General information about system operation
- `WARN`: Warning conditions that should be addressed
- `ERROR`: Error conditions that prevent normal operation
