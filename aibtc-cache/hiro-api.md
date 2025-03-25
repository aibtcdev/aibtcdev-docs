# Hiro API

The Hiro API Durable Object provides a caching layer for the Hiro API, which is the primary API service for the Stacks blockchain. It handles rate limiting, caching, and automatic retries for requests to the Hiro API.

## Base Path

All Hiro API endpoints are available under:
```
/hiro-api
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/extended` | Access to the extended API endpoints |
| `/v2/info` | Get information about the Stacks blockchain |
| `/extended/v1/address/{address}/balances` | Get balance information for a Stacks address |
| `/extended/v1/address/{address}/assets` | Get asset information for a Stacks address |
| `/known-addresses` | List all addresses being tracked by the cache |

## Response Format

All endpoints return responses in a standardized format:

### Success Response
```json
{
  "success": true,
  "data": {
    // The actual response data from the Hiro API
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

## Get Address Balances

Retrieves balance information for a Stacks address.

### Endpoint

```
GET /hiro-api/extended/v1/address/{address}/balances
```

### Path Parameters
- `address`: The Stacks address to look up

### Example Requests

#### cURL

```bash
curl https://cache.aibtc.dev/hiro-api/extended/v1/address/SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF/balances
```

#### JavaScript

```javascript
async function getAddressBalances(address) {
  const response = await fetch(
    `https://cache.aibtc.dev/hiro-api/extended/v1/address/${address}/balances`
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getAddressBalances('SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF')
  .then(balances => console.log('Address balances:', balances))
  .catch(error => console.error('Error:', error));
```

#### Python

```python
import requests

def get_address_balances(address):
    url = f'https://cache.aibtc.dev/hiro-api/extended/v1/address/{address}/balances'
    
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
    balances = get_address_balances('SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF')
    print(f"STX balance: {balances['stx']['balance']} microSTX")
except Exception as e:
    print(f"Error: {e}")
```

## Get Known Addresses

Lists all addresses that have been accessed through the cache.

### Endpoint

```
GET /hiro-api/known-addresses
```

### Example Response

```json
{
  "success": true,
  "data": {
    "stats": {
      "storage": 10,
      "cached": 8,
      "uncached": 2
    },
    "addresses": {
      "storage": [
        "SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF",
        "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
        // ... other addresses
      ],
      "cached": [
        "SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF",
        "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
        // ... other cached addresses
      ],
      "uncached": [
        // ... addresses not in cache
      ]
    }
  }
}
```
