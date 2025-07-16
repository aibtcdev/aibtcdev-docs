# Clarity Value Types

The AIBTC Cache supports two ways to specify Clarity values:

1. **Stacks.js Clarity Values**: Using the native Clarity value objects from the `@stacks/transactions` library
2. **Simplified JSON Format**: A JSON-friendly format that's easier to use from non-TypeScript environments

This document focuses on the simplified JSON format, which can be used when specifying function arguments or interpreting decoded values.

## Simplified Format vs. Stacks.js Format

**Stacks.js Format**:
```javascript
import { uintCV, stringAsciiCV, tupleCV } from '@stacks/transactions';

// Create Clarity values using Stacks.js
const args = [
  uintCV(123),
  stringAsciiCV("hello"),
  tupleCV({
    key1: uintCV(456),
    key2: stringAsciiCV("world")
  })
];
```

**Simplified JSON Format**:
```javascript
// Equivalent values using the simplified format
const args = [
  { type: "uint", value: "123" },
  { type: "string", value: "hello" },
  { 
    type: "tuple", 
    value: {
      key1: { type: "uint", value: "456" },
      key2: { type: "string", value: "world" }
    }
  }
];
```

When specifying function arguments or decoding values, you can use the following Clarity value types:

## Basic Types

| Type                      | Description         | Example                                                                       |
| ------------------------- | ------------------- | ----------------------------------------------------------------------------- |
| `uint`                    | Unsigned integer    | `{"type": "uint", "value": "123"}`                                            |
| `int`                     | Signed integer      | `{"type": "int", "value": "-123"}`                                            |
| `bool`                    | Boolean             | `{"type": "bool", "value": true}`                                             |
| `principal`               | Principal (address) | `{"type": "principal", "value": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA"}` |
| `buffer`                  | Byte buffer         | `{"type": "buffer", "value": "0x68656c6c6f"}`                                 |
| `string` or `stringascii` | ASCII string        | `{"type": "string", "value": "hello"}`                                        |
| `stringutf8`              | UTF-8 string        | `{"type": "stringutf8", "value": "hello 世界"}`                               |

## Container Types

| Type    | Description     | Example                                                                                       |
| ------- | --------------- | --------------------------------------------------------------------------------------------- |
| `list`  | List of values  | `{"type": "list", "value": [{"type": "uint", "value": "1"}, {"type": "uint", "value": "2"}]}` |
| `tuple` | Key-value pairs | `{"type": "tuple", "value": {"key1": {"type": "uint", "value": "1"}}}`                        |

## Optional Types

| Type                 | Description   | Example                                                       |
| -------------------- | ------------- | ------------------------------------------------------------- |
| `none`               | Optional none | `{"type": "none"}`                                            |
| `some` or `optional` | Optional some | `{"type": "some", "value": {"type": "uint", "value": "123"}}` |

## Response Types

| Type                   | Description    | Example                                                      |
| ---------------------- | -------------- | ------------------------------------------------------------ |
| `ok` or `responseok`   | Response OK    | `{"type": "ok", "value": {"type": "uint", "value": "123"}}`  |
| `err` or `responseerr` | Response Error | `{"type": "err", "value": {"type": "uint", "value": "123"}}` |

## Complex Examples

### Nested Tuple with List

```json
{
  "type": "tuple",
  "value": {
    "name": {
      "type": "string",
      "value": "Example DAO"
    },
    "members": {
      "type": "list",
      "value": [
        {
          "type": "principal",
          "value": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM"
        },
        {
          "type": "principal",
          "value": "ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG"
        }
      ]
    }
  }
}
```

### Response with Optional

```json
{
  "type": "responseOk",
  "value": {
    "type": "some",
    "value": {
      "type": "tuple",
      "value": {
        "id": {
          "type": "uint",
          "value": "123"
        },
        "active": {
          "type": "bool",
          "value": true
        }
      }
    }
  }
}
```

### BigInt Handling

When working with large numbers, they are represented as strings to avoid precision loss:

```json
{
  "type": "uint",
  "value": "9007199254740992"
}
```
