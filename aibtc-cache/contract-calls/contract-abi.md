# Contract ABI

This endpoint retrieves the ABI (Application Binary Interface) for a smart contract. ABIs are cached indefinitely after the first request.

## Endpoint

```
GET /contract-calls/abi/{contractAddress}/{contractName}
```

## Path Parameters
- `contractAddress`: The principal address of the contract
- `contractName`: The name of the contract

## Response
The contract's ABI in JSON format.

## Example Request

```bash
curl https://cache.aibtc.dev/contract-calls/abi/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-core-proposals-v2
```

## Example Response

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
