# Utilities

The AIBTC Cache system includes several utility modules that provide common functionality used across the caching services.

## Request/Response Utilities

The `requests-responses-util.ts` module provides utilities for handling HTTP requests and responses.

### Functions

#### `corsHeaders(origin?: string): HeadersInit`

Creates CORS headers for cross-origin requests.

**Parameters:**
- `origin` (optional): Origin to allow, defaults to '*' (all origins)

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
- 
**Returns:** Response object with standardized format: `{ success: false, error: { id, code, message, details } }`

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
- 
**Returns:** Response object with standardized format: `{ success: false, error: { id, code, message, details } }`

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

The `logger.ts` module provides logging capabilities across the application.

### Classes

#### `Logger`

Simple logger that writes to console and optionally to KV storage.

**Methods:**
- `getInstance(env?: Env): Logger`: Get the singleton logger instance
- `log(level: LogLevel, message: string, context?: Record<string, any>, error?: Error, duration?: number): string`: Log a message
- `debug(message: string, context?: Record<string, any>, duration?: number): string`: Log a debug message
- `info(message: string, context?: Record<string, any>, duration?: number): string`: Log an info message
- `warn(message: string, context?: Record<string, any>, duration?: number): string`: Log a warning message
- `error(message: string, error?: Error, context?: Record<string, any>, duration?: number): string`: Log an error message

### Enums

#### `LogLevel`

Log levels in order of increasing severity:
- `DEBUG`
- `INFO`
- `WARN`
- `ERROR`

## Address Store Utilities

The `address-store-util.ts` module provides utilities for managing Stacks addresses.

### Functions

#### `getKnownAddresses(env: Env): Promise<string[]>`

Retrieves the list of known Stacks addresses from KV storage.

**Parameters:**
- `env`: The Cloudflare Worker environment

**Returns:** Array of known Stacks addresses

#### `addKnownAddress(env: Env, address: string): Promise<void>`

Adds a Stacks address to the list of known addresses in KV storage.
Only adds the address if it's not already in the list.

**Parameters:**
- `env`: The Cloudflare Worker environment
- `address`: The Stacks address to add
