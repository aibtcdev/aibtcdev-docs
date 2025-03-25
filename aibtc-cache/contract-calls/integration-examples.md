# Integration Examples

## Frontend Integration

For frontend applications using the Stacks.js library, you can build the `functionArgs` the same way you would for `fetchCallReadOnlyFunction`. The cache accepts the exact same Clarity value objects created by Stacks.js functions like `uintCV()` or `cl.uint()`.

```javascript
import { 
  callReadOnlyFunction, 
  cvToValue,
  uintCV
} from '@stacks/transactions';
// Or using the clarity namespace
// import { Cl } from '@stacks/transactions';

// Using Stacks.js directly (without cache)
const result = await callReadOnlyFunction({
  contractAddress: 'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA',
  contractName: 'media3-action-proposals-v2',
  functionName: 'get-proposal',
  functionArgs: [uintCV(3)],
  network: 'testnet',
});
const decodedResult = cvToValue(result);

// Using the cache service with the same Stacks.js Clarity values
const response = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    functionArgs: [uintCV(3)]  // Use the same Stacks.js Clarity values directly
  })
});
const decodedResult = await response.json();

// Alternatively, you can use the simplified format
const responseAlt = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    functionArgs: [
      {
        type: 'uint',
        value: '3'
      }
    ]
  })
});
const decodedResultAlt = await responseAlt.json();
```

## Backend Integration

For backend applications in Python, you can use the simplified format without needing any Stacks-specific libraries:

```python
import requests
import json

def get_proposal(proposal_id):
    """
    Fetch a proposal from the contract using the cache service.
    
    Args:
        proposal_id (int): The ID of the proposal to fetch
        
    Returns:
        dict: The proposal data
    """
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
    
    # Raise an exception for HTTP errors
    response.raise_for_status()
    
    return response.json()

def get_token_balance(address, token_contract_address, token_contract_name):
    """
    Fetch a token balance for an address.
    
    Args:
        address (str): The Stacks address to check
        token_contract_address (str): The contract address of the token
        token_contract_name (str): The contract name of the token
        
    Returns:
        dict: The balance data
    """
    url = f'https://cache.aibtc.dev/contract-calls/read-only/{token_contract_address}/{token_contract_name}/get-balance'
    
    payload = {
        "functionArgs": [
            {
                "type": "principal",
                "value": address
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

# Usage examples
if __name__ == "__main__":
    try:
        # Get proposal with ID 3
        proposal = get_proposal(3)
        print(f"Proposal data: {json.dumps(proposal, indent=2)}")
        
        # Get token balance for an address
        balance = get_token_balance(
            "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
            "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
            "media3-token"
        )
        print(f"Token balance: {balance}")
        
    except requests.exceptions.RequestException as e:
        print(f"Error making request: {e}")
```
