# Decode Clarity Value

This endpoint decodes a Clarity value into a JavaScript/JSON representation. It accepts both Clarity value objects and serialized hexadecimal strings.

## Endpoint

```
POST /contract-calls/decode-clarity-value
```

## Request Body
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

Or with a serialized string:

```json
{
  "clarityValue": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321",
  "strictJsonCompat": true,
  "preserveContainers": false
}
```

## Request Body Parameters
- `clarityValue`: The Clarity value to decode (can be a serialized hexadecimal string or a Clarity value object)
- `strictJsonCompat` (optional): Whether to ensure values are JSON compatible (defaults to `true`)
- `preserveContainers` (optional): Whether to preserve container types in the output (defaults to `false`)

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {
    "original": {
      "type": "responseOk",
      "value": {
        "type": "uint",
        "value": "123"
      }
    },
    "decoded": 123
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
- `VALIDATION_ERROR` - The Clarity value format is invalid or unsupported

## Example Requests

### cURL - Clarity Value Object

```bash
curl -X POST \
  https://cache.aibtc.dev/contract-calls/decode-clarity-value \
  -H "Content-Type: application/json" \
  -d '{"clarityValue": { "type": "uint", "value": "1000" }}' \
  -w "\n"
```

### cURL - Serialized String

```bash
curl -X POST \
  https://cache.aibtc.dev/contract-calls/decode-clarity-value \
  -H "Content-Type: application/json" \
  -d '{"clarityValue": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321"}' \
  -w "\n"
```

### Node.js

```javascript
async function decodeClarityValue(clarityValue) {
  const response = await fetch(
    'https://cache.aibtc.dev/contract-calls/decode-clarity-value',
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ clarityValue }),
    }
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage with Clarity Value Object
decodeClarityValue({ type: "uint", value: "1000" })
  .then(data => console.log('Decoded value:', data.decoded))
  .catch(error => console.error('Error:', error));

// Usage with Serialized String
decodeClarityValue("0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321")
  .then(data => console.log('Decoded value:', data.decoded))
  .catch(error => console.error('Error:', error));
```

### Python

```python
import requests
import json

def decode_clarity_value(clarity_value):
    url = 'https://cache.aibtc.dev/contract-calls/decode-clarity-value'
    
    payload = {
        "clarityValue": clarity_value
    }
    
    response = requests.post(
        url,
        headers={'Content-Type': 'application/json'},
        data=json.dumps(payload)
    )
    
    response.raise_for_status()
    result = response.json()
    
    if result.get('success'):
        return result['data']
    else:
        error = result.get('error', {})
        raise Exception(f"API Error: {error.get('code')} - {error.get('message')}")

# Usage with Clarity Value Object
try:
    data = decode_clarity_value({"type": "uint", "value": "1000"})
    print(f"Original: {json.dumps(data['original'], indent=2)}")
    print(f"Decoded: {data['decoded']}")
except Exception as e:
    print(f"Error: {e}")

# Usage with Serialized String
try:
    hex_string = "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321"
    data = decode_clarity_value(hex_string)
    print(f"Original: {data['original']}")
    print(f"Decoded: {data['decoded']}")
except Exception as e:
    print(f"Error: {e}")
```

## Example Responses

### Success Response for Clarity Value Object
```json
{
  "success": true,
  "data": {
    "original": {
      "type": "uint",
      "value": "1000"
    },
    "decoded": 1000
  }
}
```

### Success Response for Serialized String
```json
{
  "success": true,
  "data": {
    "original": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321",
    "decoded": "Exciting news, DAO members! Our project is making fantastic progress, and we're thrilled to share the latest updates with you all. Stay tuned for more details!"
  }
}
```

### Error Response Example
```json
{
  "success": false,
  "error": {
    "id": "a1b2c3",
    "code": "VALIDATION_ERROR",
    "message": "Failed to convert to Clarity value of type invalid_type",
    "details": {
      "valueType": "invalid_type",
      "error": "Unsupported clarity type: invalid_type"
    }
  }
}
```
