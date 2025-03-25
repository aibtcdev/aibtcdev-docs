# BNS API

The BNS (Blockchain Name System) API provides access to BNS name data for Stacks addresses. It allows you to look up the BNS name associated with a Stacks address.

## Base Path

All BNS API endpoints are available under:
```
/bns
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/names/{address}` | Get the BNS name for a Stacks address |

## Response Format

All endpoints return responses in a standardized format:

### Success Response
```json
{
  "success": true,
  "data": "name.btc" // or just the string directly for simple responses
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

## Get BNS Name for Address

Retrieves the BNS name associated with a Stacks address.

### Endpoint

```
GET /bns/names/{address}
```

### Path Parameters
- `address`: The Stacks address to look up

### Example Requests

#### cURL

```bash
curl https://cache.aibtc.dev/bns/names/SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF
```

#### JavaScript

```javascript
async function getBnsName(address) {
  const response = await fetch(
    `https://cache.aibtc.dev/bns/names/${address}`
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getBnsName('SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF')
  .then(name => console.log('BNS Name:', name))
  .catch(error => console.error('Error:', error));
```

#### Python

```python
import requests

def get_bns_name(address):
    url = f'https://cache.aibtc.dev/bns/names/{address}'
    
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
    name = get_bns_name('SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF')
    print(f"BNS Name: {name}")
except Exception as e:
    print(f"Error: {e}")
```

### Example Response

#### Success Response (Name Found)
```json
{
  "success": true,
  "data": "muneeb.btc"
}
```

#### Success Response (No Name)
```json
{
  "success": false,
  "error": {
    "id": "a1b2c3",
    "code": "NOT_FOUND",
    "message": "No registered name found",
    "details": {
      "resource": "name for address SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF",
      "reason": "No registered name found"
    }
  }
}
```

#### Error Response (Invalid Address)
```json
{
  "success": false,
  "error": {
    "id": "d4e5f6",
    "code": "INVALID_REQUEST",
    "message": "Invalid address SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF1, valid Stacks address required",
    "details": {
      "reason": "Invalid address SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF1, valid Stacks address required"
    }
  }
}
```
