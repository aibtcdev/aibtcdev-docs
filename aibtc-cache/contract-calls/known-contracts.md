# Known Contracts

This endpoint lists all contracts that have been accessed through the cache and have their ABIs stored in the contract ABI cache.

## Endpoint

```
GET /contract-calls/known-contracts
```

## Example Requests

### cURL

```bash
curl https://cache.aibtc.dev/contract-calls/known-contracts
```

### Node.js

```javascript
async function getKnownContracts() {
  const response = await fetch(
    'https://cache.aibtc.dev/contract-calls/known-contracts'
  );
  
  return response.json();
}

// Usage
getKnownContracts()
  .then(contracts => console.log('Known contracts:', contracts))
  .catch(error => console.error('Error:', error));
```

### Python

```python
import requests
import json

def get_known_contracts():
    url = 'https://cache.aibtc.dev/contract-calls/known-contracts'
    
    response = requests.get(url)
    response.raise_for_status()
    return response.json()

# Usage
try:
    contracts = get_known_contracts()
    print(f"Known contracts: {json.dumps(contracts, indent=2)}")
except requests.exceptions.RequestException as e:
    print(f"Error making request: {e}")
```

## Response

### Current Format
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

### Alternative Format (String Array)
```json
{
  "stats": {
    "total": 10,
    "cached": 10
  },
  "contracts": {
    "cached": [
      "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media3-core-proposals-v2",
      "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media3-faktory",
      // ... other contracts
    ]
  }
}
```
