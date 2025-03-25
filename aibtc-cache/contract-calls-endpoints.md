# Contract Calls Endpoints

The Contract Calls Durable Object provides a caching layer for interacting with Stacks smart contracts. It allows you to make read-only function calls to any Stacks smart contract while benefiting from caching, rate limiting, and automatic retries.

## Base Path

All contract call endpoints are available under:
```
/contract-calls
```

## Available Endpoints

### Read-Only Function Calls

```
POST /contract-calls/read-only/{contractAddress}/{contractName}/{functionName}
```

Makes a read-only call to a smart contract function. The response is cached for future requests.

#### Path Parameters
- `contractAddress`: The principal address of the contract (e.g., `ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA`)
- `contractName`: The name of the contract (e.g., `media3-action-proposals-v2`)
- `functionName`: The name of the function to call (e.g., `get-proposal`)

#### Request Body
```json
{
  "functionArgs": [
    {
      "type": "uint",
      "value": "3"
    }
  ],
  "network": "testnet",
  "senderAddress": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
  "strictJsonCompat": true,
  "preserveContainers": false
}
```

#### Request Body Parameters
- `functionArgs`: Array of arguments to pass to the function (using simplified Clarity value format)
- `network` (optional): The Stacks network to use (`mainnet` or `testnet`, defaults to `testnet`)
- `senderAddress` (optional): The address to use as the sender (defaults to the contract address)
- `strictJsonCompat` (optional): Whether to ensure values are JSON compatible (defaults to `true`)
- `preserveContainers` (optional): Whether to preserve container types in the output (defaults to `false`)

#### Response
The function's return value, decoded from Clarity format to JavaScript/JSON.

#### Example Request (cURL)

```bash
curl -X POST \
  https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal \
  -H "Content-Type: application/json" \
  -d '{"functionArgs": [{ "type": "uint", "value": "3" }]}' \
  -w "\n"
```

#### Example Response

```json
{
  "action": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media3-action-send-message",
  "bond": "100000000000",
  "caller": "ST1F8Z1TDZQVP9P0D05VAW5MHKS2EYXZZ1PDE9Q8A",
  "concluded": false,
  "createdAt": "586130",
  "creator": "ST1F8Z1TDZQVP9P0D05VAW5MHKS2EYXZZ1PDE9Q8A",
  "endBlock": "27570",
  "executed": false,
  "liquidTokens": "2104509663564782",
  "metQuorum": false,
  "metThreshold": false,
  "parameters": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321",
  "passed": false,
  "startBlock": "27566",
  "votesAgainst": "650503728846681",
  "votesFor": "0"
}
```

### Contract ABI

```
GET /contract-calls/abi/{contractAddress}/{contractName}
```

Retrieves the ABI (Application Binary Interface) for a smart contract. ABIs are cached indefinitely after the first request.

#### Path Parameters
- `contractAddress`: The principal address of the contract
- `contractName`: The name of the contract

#### Response
The contract's ABI in JSON format.

#### Example Request

```bash
curl https://cache.aibtc.dev/contract-calls/abi/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-core-proposals-v2
```

#### Example Response

```json
{
  "functions": [
    {
      "name": "get-proposal",
      "access": "read_only",
      "args": [
        {
          "name": "id",
          "type": "uint128"
        }
      ],
      "outputs": {
        "type": {
          "tuple": [
            {
              "name": "action",
              "type": "principal"
            },
            {
              "name": "bond",
              "type": "uint128"
            },
            // ... other fields
          ]
        }
      }
    },
    // ... other functions
  ],
  "variables": [
    // ... contract variables
  ],
  "maps": [
    // ... contract maps
  ],
  "fungible_tokens": [],
  "non_fungible_tokens": []
}
```

### Known Contracts

```
GET /contract-calls/known-contracts
```

Lists all contracts that have been accessed through the cache.

#### Response
```json
{
  "stats": {
    "total": 10,
    "cached": 10
  },
  "contracts": {
    "cached": [
      {
        "contractAddress": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
        "contractName": "media3-core-proposals-v2"
      },
      {
        "contractAddress": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
        "contractName": "media3-faktory"
      },
      // ... other contracts
    ]
  }
}
```

### Decode Clarity Value

```
POST /contract-calls/decode-clarity-value
```

Decodes a Clarity value into a JavaScript/JSON representation.

#### Request Body
```json
{
  "clarityValue": {
    "type": "responseOk",
    "value": {
      "type": "uint",
      "value": "123"
    }
  },
  "strictJsonCompat": true,
  "preserveContainers": false
}
```

#### Request Body Parameters
- `clarityValue`: The Clarity value to decode (can be a serialized string or an object)
- `strictJsonCompat` (optional): Whether to ensure values are JSON compatible (defaults to `true`)
- `preserveContainers` (optional): Whether to preserve container types in the output (defaults to `false`)

#### Response
```json
{
  "original": {
    "type": "responseOk",
    "value": {
      "type": "uint",
      "value": "123"
    }
  },
  "decoded": 123
}
```

## Clarity Value Types

When specifying function arguments or decoding values, you can use the following Clarity value types:

| Type | Description | Example |
|------|-------------|---------|
| `uint` | Unsigned integer | `{"type": "uint", "value": "123"}` |
| `int` | Signed integer | `{"type": "int", "value": "-123"}` |
| `bool` | Boolean | `{"type": "bool", "value": true}` |
| `principal` | Principal (address) | `{"type": "principal", "value": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA"}` |
| `buffer` | Byte buffer | `{"type": "buffer", "value": "0x68656c6c6f"}` |
| `string` or `stringascii` | ASCII string | `{"type": "string", "value": "hello"}` |
| `stringutf8` | UTF-8 string | `{"type": "stringutf8", "value": "hello 世界"}` |
| `list` | List of values | `{"type": "list", "value": [{"type": "uint", "value": "1"}, {"type": "uint", "value": "2"}]}` |
| `tuple` | Key-value pairs | `{"type": "tuple", "value": {"key1": {"type": "uint", "value": "1"}}}` |
| `none` | Optional none | `{"type": "none"}` |
| `some` or `optional` | Optional some | `{"type": "some", "value": {"type": "uint", "value": "123"}}` |
| `ok` or `responseok` | Response OK | `{"type": "ok", "value": {"type": "uint", "value": "123"}}` |
| `err` or `responseerr` | Response Error | `{"type": "err", "value": {"type": "uint", "value": "123"}}` |

## Frontend Integration

For frontend applications using the Stacks.js library, you can build the `functionArgs` the same way you would for `fetchCallReadOnlyFunction`. The cache accepts an array of `ClarityValue[]` objects.

```javascript
import { 
  callReadOnlyFunction, 
  cvToValue,
  uintCV
} from '@stacks/transactions';

// Using Stacks.js directly (without cache)
const result = await callReadOnlyFunction({
  contractAddress: 'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA',
  contractName: 'media3-action-proposals-v2',
  functionName: 'get-proposal',
  functionArgs: [uintCV(3)],
  network: 'testnet',
});
const decodedResult = cvToValue(result);

// Using the cache service
const response = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    functionArgs: [
      {
        type: 'uint',
        value: '3'
      }
    ]
  })
});
const decodedResult = await response.json();
```

## Backend Integration

For backend applications, you can use the simplified Clarity value format:

```javascript
// Node.js example using fetch
const fetch = require('node-fetch');

async function getProposal(id) {
  const response = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      functionArgs: [
        {
          type: 'uint',
          value: id.toString()
        }
      ]
    })
  });
  
  return response.json();
}

// Usage
getProposal(3).then(proposal => console.log(proposal));
```
