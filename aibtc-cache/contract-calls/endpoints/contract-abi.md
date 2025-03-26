# Contract ABI

This endpoint retrieves the ABI (Application Binary Interface) for a smart contract. ABIs are cached indefinitely after the first request.

## Endpoint

```
GET /contract-calls/abi/{contractAddress}/{contractName}
```

## Path Parameters
- `contractAddress`: The principal address of the contract (e.g., `ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA` for testnet or `SP252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA` for mainnet)
- `contractName`: The name of the contract

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {
    "functions": [...],
    "variables": [...],
    "maps": [...],
    "fungible_tokens": [...],
    "non_fungible_tokens": [...],
    "epoch": "Epoch31",
    "clarity_version": "Clarity3"
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

## Common Error Codes
- `INVALID_CONTRACT_ADDRESS` - The contract address is not a valid Stacks address
- `UPSTREAM_API_ERROR` - Error from the Stacks API when fetching the ABI

## Example Requests

### cURL

```bash
curl https://cache.aibtc.dev/contract-calls/abi/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-core-proposals-v2
```

### Node.js

```javascript
async function getContractAbi(contractAddress, contractName) {
  const response = await fetch(
    `https://cache.aibtc.dev/contract-calls/abi/${contractAddress}/${contractName}`
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getContractAbi(
  'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA',
  'media3-core-proposals-v2'
)
  .then(abi => console.log('Contract ABI:', abi))
  .catch(error => console.error('Error:', error));
```

### Python

```python
import requests
import json

def get_contract_abi(contract_address, contract_name):
    url = f'https://cache.aibtc.dev/contract-calls/abi/{contract_address}/{contract_name}'
    
    response = requests.get(url)
    response.raise_for_status()
    result = response.json()
    
    if result.get('success'):
        return result['data']
    else:
        error = result.get('error', {})
        raise Exception(f"API Error: {error.get('code')} - {error.get('message')}")

# Usage
try:
    abi = get_contract_abi(
        'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA',
        'media3-core-proposals-v2'
    )
    print(f"Contract ABI: {json.dumps(abi, indent=2)}")
except Exception as e:
    print(f"Error: {e}")
```

## Example Response

### Core Proposals Contract ABI

```json
{
  "functions": [
    {
      "name": "get-block-hash",
      "access": "private",
      "args": [
        {
          "name": "blockHeight",
          "type": "uint128"
        }
      ],
      "outputs": {
        "type": {
          "optional": {
            "buffer": {
              "length": 32
            }
          }
        }
      }
    },
    {
      "name": "is-dao-or-extension",
      "access": "private",
      "args": [],
      "outputs": {
        "type": {
          "response": {
            "ok": "bool",
            "error": "uint128"
          }
        }
      }
    },
    {
      "name": "get-proposal",
      "access": "read_only",
      "args": [
        {
          "name": "proposal",
          "type": "principal"
        }
      ],
      "outputs": {
        "type": {
          "optional": {
            "tuple": [
              {
                "name": "bond",
                "type": "uint128"
              },
              {
                "name": "caller",
                "type": "principal"
              },
              {
                "name": "concluded",
                "type": "bool"
              },
              {
                "name": "createdAt",
                "type": "uint128"
              },
              {
                "name": "creator",
                "type": "principal"
              },
              {
                "name": "endBlock",
                "type": "uint128"
              },
              {
                "name": "executed",
                "type": "bool"
              },
              {
                "name": "liquidTokens",
                "type": "uint128"
              },
              {
                "name": "metQuorum",
                "type": "bool"
              },
              {
                "name": "metThreshold",
                "type": "bool"
              },
              {
                "name": "passed",
                "type": "bool"
              },
              {
                "name": "startBlock",
                "type": "uint128"
              },
              {
                "name": "votesAgainst",
                "type": "uint128"
              },
              {
                "name": "votesFor",
                "type": "uint128"
              }
            ]
          }
        }
      }
    },
    {
      "name": "vote-on-proposal",
      "access": "public",
      "args": [
        {
          "name": "proposal",
          "type": "trait_reference"
        },
        {
          "name": "vote",
          "type": "bool"
        }
      ],
      "outputs": {
        "type": {
          "response": {
            "ok": "bool",
            "error": "uint128"
          }
        }
      }
    }
  ],
  "variables": [
    {
      "name": "ERR_ALREADY_VOTED",
      "type": {
        "response": {
          "ok": "none",
          "error": "uint128"
        }
      },
      "access": "constant"
    },
    {
      "name": "VOTING_DELAY",
      "type": "uint128",
      "access": "constant"
    },
    {
      "name": "VOTING_PERIOD",
      "type": "uint128",
      "access": "constant"
    },
    {
      "name": "proposalBond",
      "type": "uint128",
      "access": "variable"
    }
  ],
  "maps": [
    {
      "name": "Proposals",
      "key": "principal",
      "value": {
        "tuple": [
          {
            "name": "bond",
            "type": "uint128"
          },
          {
            "name": "caller",
            "type": "principal"
          },
          {
            "name": "concluded",
            "type": "bool"
          },
          {
            "name": "createdAt",
            "type": "uint128"
          },
          {
            "name": "creator",
            "type": "principal"
          },
          {
            "name": "endBlock",
            "type": "uint128"
          },
          {
            "name": "executed",
            "type": "bool"
          },
          {
            "name": "liquidTokens",
            "type": "uint128"
          },
          {
            "name": "metQuorum",
            "type": "bool"
          },
          {
            "name": "metThreshold",
            "type": "bool"
          },
          {
            "name": "passed",
            "type": "bool"
          },
          {
            "name": "startBlock",
            "type": "uint128"
          },
          {
            "name": "votesAgainst",
            "type": "uint128"
          },
          {
            "name": "votesFor",
            "type": "uint128"
          }
        ]
      }
    }
  ],
  "fungible_tokens": [],
  "non_fungible_tokens": [],
  "epoch": "Epoch31",
  "clarity_version": "Clarity3"
}
```

### Token Contract ABI Example

```bash
curl https://cache.aibtc.dev/contract-calls/abi/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-faktory
```

```json
{
  "functions": [
    {
      "name": "get-balance",
      "access": "read_only",
      "args": [
        {
          "name": "account",
          "type": "principal"
        }
      ],
      "outputs": {
        "type": {
          "response": {
            "ok": "uint128",
            "error": "none"
          }
        }
      }
    },
    {
      "name": "get-name",
      "access": "read_only",
      "args": [],
      "outputs": {
        "type": {
          "response": {
            "ok": {
              "string-ascii": {
                "length": 13
              }
            },
            "error": "none"
          }
        }
      }
    },
    {
      "name": "get-symbol",
      "access": "read_only",
      "args": [],
      "outputs": {
        "type": {
          "response": {
            "ok": {
              "string-ascii": {
                "length": 6
              }
            },
            "error": "none"
          }
        }
      }
    },
    {
      "name": "transfer",
      "access": "public",
      "args": [
        {
          "name": "amount",
          "type": "uint128"
        },
        {
          "name": "sender",
          "type": "principal"
        },
        {
          "name": "recipient",
          "type": "principal"
        },
        {
          "name": "memo",
          "type": {
            "optional": {
              "buffer": {
                "length": 34
              }
            }
          }
        }
      ],
      "outputs": {
        "type": {
          "response": {
            "ok": "bool",
            "error": "uint128"
          }
        }
      }
    }
  ],
  "variables": [
    {
      "name": "ERR-NOT-AUTHORIZED",
      "type": "uint128",
      "access": "constant"
    },
    {
      "name": "MAX",
      "type": "uint128",
      "access": "constant"
    },
    {
      "name": "contract-owner",
      "type": "principal",
      "access": "variable"
    }
  ],
  "maps": [],
  "fungible_tokens": [
    {
      "name": "MEDIA3"
    }
  ],
  "non_fungible_tokens": [],
  "epoch": "Epoch31",
  "clarity_version": "Clarity3"
}
```
