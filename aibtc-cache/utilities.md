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

#### `createJsonResponse(body: unknown, status = 200): Response`

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

**Parameters:**
- `arg`: Either a ClarityValue object or a simplified representation

**Returns:** A proper ClarityValue object

**Throws:** Error if the type is unsupported or the conversion fails

## Stacks Network Utilities

The `stacks-network-util.ts` module provides utilities for working with Stacks networks.

### Functions

#### `getNetworkByPrincipal(principal: string): StacksNetworkName`

Determines the network (mainnet or testnet) based on a principal address.

**Parameters:**
- `principal`: A Stacks principal address

**Returns:** The network name ('mainnet' or 'testnet')
