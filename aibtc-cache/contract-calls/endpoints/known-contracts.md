# Known Contracts

This endpoint lists all contracts that have been accessed through the cache and have their ABIs stored in the contract ABI cache. Contracts from both mainnet and testnet are included. This endpoint is fast and doesn't require any external API calls as all data is stored locally.

## Endpoint

```
GET /contract-calls/known-contracts
```

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {
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
}
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
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getKnownContracts()
  .then(data => {
    console.log(`Total contracts: ${data.stats.total}`);
    console.log('Known contracts:', data.contracts.cached);
  })
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
    result = response.json()
    
    if result.get('success'):
        return result['data']
    else:
        error = result.get('error', {})
        raise Exception(f"API Error: {error.get('code')} - {error.get('message')}")

# Usage
try:
    data = get_known_contracts()
    print(f"Total contracts: {data['stats']['total']}")
    print(f"Known contracts: {json.dumps(data['contracts']['cached'], indent=2)}")
except Exception as e:
    print(f"Error: {e}")
```
