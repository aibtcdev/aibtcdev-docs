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

## Response
For a Clarity value object:
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

For a serialized string (containing a UTF-8 string in this example):
```json
{
  "original": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321",
  "decoded": "Exciting news, DAO members! Our project is making fantastic progress, and we're thrilled to share the latest updates with you all. Stay tuned for more details!"
}
```

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
  
  return response.json();
}

// Usage with Clarity Value Object
decodeClarityValue({ type: "uint", value: "1000" })
  .then(result => console.log('Decoded value:', result))
  .catch(error => console.error('Error:', error));

// Usage with Serialized String
decodeClarityValue("0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321")
  .then(result => console.log('Decoded value:', result))
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
    return response.json()

# Usage with Clarity Value Object
try:
    result = decode_clarity_value({"type": "uint", "value": "1000"})
    print(f"Decoded value: {json.dumps(result, indent=2)}")
except requests.exceptions.RequestException as e:
    print(f"Error making request: {e}")

# Usage with Serialized String
try:
    hex_string = "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321"
    result = decode_clarity_value(hex_string)
    print(f"Decoded value: {json.dumps(result, indent=2)}")
except requests.exceptions.RequestException as e:
    print(f"Error making request: {e}")
```

## Example Responses

### For Clarity Value Object
```json
{
  "original": {
    "type": "uint",
    "value": "1000"
  },
  "decoded": "1000"
}
```

### For Serialized String
```json
{
  "original": "0x0d0000009f4578636974696e67206e6577732c2044414f206d656d6265727321204f75722070726f6a656374206973206d616b696e672066616e7461737469632070726f67726573732c20616e6420776527726520746872696c6c656420746f20736861726520746865206c61746573742075706461746573207769746820796f7520616c6c2e20537461792074756e656420666f72206d6f72652064657461696c7321",
  "decoded": "Exciting news, DAO members! Our project is making fantastic progress, and we're thrilled to share the latest updates with you all. Stay tuned for more details!"
}
```
