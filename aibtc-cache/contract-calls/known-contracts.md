# Known Contracts

This endpoint lists all contracts that have been accessed through the cache.

## Endpoint

```
GET /contract-calls/known-contracts
```

## Response
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
