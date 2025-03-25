# Read-Only Function Calls

This endpoint allows you to make read-only calls to smart contract functions. The response is cached for future requests.

## Endpoint

```
POST /contract-calls/read-only/{contractAddress}/{contractName}/{functionName}
```

## Path Parameters
- `contractAddress`: The principal address of the contract (e.g., `ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA`)
- `contractName`: The name of the contract (e.g., `media3-action-proposals-v2`)
- `functionName`: The name of the function to call (e.g., `get-proposal`)

## Request Body
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

## Request Body Parameters
- `functionArgs`: Array of arguments to pass to the function (using simplified Clarity value format)
- `network` (optional): The Stacks network to use (`mainnet` or `testnet`, defaults to `testnet`)
- `senderAddress` (optional): The address to use as the sender (defaults to the contract address)
- `strictJsonCompat` (optional): Whether to ensure values are JSON compatible (defaults to `true`)
- `preserveContainers` (optional): Whether to preserve container types in the output (defaults to `false`)

## Response
The function's return value, decoded from Clarity format to JavaScript/JSON.

## Example Requests

### cURL

```bash
curl -X POST \
  https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal \
  -H "Content-Type: application/json" \
  -d '{"functionArgs": [{ "type": "uint", "value": "3" }]}' \
  -w "\n"
```

### Node.js with Stacks.js

```javascript
import { uintCV } from '@stacks/transactions';
// Or using the clarity namespace: import { clarity as cl } from '@stacks/transactions';

async function getProposal(proposalId) {
  // Create function arguments using Stacks.js
  const functionArgs = [uintCV(proposalId)];
  
  const response = await fetch(
    'https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal',
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ functionArgs }),
    }
  );
  
  return response.json();
}

// Usage
getProposal(3)
  .then(proposal => console.log('Proposal:', proposal))
  .catch(error => console.error('Error:', error));
```

### Python with Simplified Format

```python
import requests
import json

def get_proposal(proposal_id):
    url = 'https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal'
    
    payload = {
        "functionArgs": [
            {
                "type": "uint",
                "value": str(proposal_id)
            }
        ]
    }
    
    response = requests.post(
        url,
        headers={'Content-Type': 'application/json'},
        data=json.dumps(payload)
    )
    
    response.raise_for_status()
    return response.json()

# Usage
try:
    proposal = get_proposal(3)
    print(f"Proposal data: {json.dumps(proposal, indent=2)}")
except requests.exceptions.RequestException as e:
    print(f"Error making request: {e}")
```

## Example Response

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
