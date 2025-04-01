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
    functionArgs: [uintCV(3)],  // Use the same Stacks.js Clarity values directly
    network: 'testnet'  // Specify the network explicitly
  })
});
const result = await response.json();
if (result.success) {
  const decodedResult = result.data;
  console.log('Proposal data:', decodedResult);
} else {
  console.error('Error:', result.error);
}

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
    ],
    network: 'testnet'
  })
});
const resultAlt = await responseAlt.json();
if (resultAlt.success) {
  const decodedResultAlt = resultAlt.data;
  console.log('Proposal data (alt):', decodedResultAlt);
} else {
  console.error('Error (alt):', resultAlt.error);
}

// Example with cache control options
const responseWithCacheControl = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
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
    ],
    network: 'mainnet',
    cacheControl: {
      bustCache: true,   // Force a fresh request, bypassing the cache
      skipCache: false,  // Whether to skip caching this result (default: false)
      ttl: 3600          // Cache this result for 1 hour (3600 seconds)
    }
  })
});
const resultWithCacheControl = await responseWithCacheControl.json();
if (resultWithCacheControl.success) {
  console.log('Fresh data with custom TTL:', resultWithCacheControl.data);
} else {
  console.error('Error:', resultWithCacheControl.error);
}

// Example with sender address specified
const responseWithSender = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-token/get-balance', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    functionArgs: [
      {
        type: 'principal',
        value: 'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA'
      }
    ],
    network: 'mainnet',
    senderAddress: 'ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA' // Optional sender address for the contract call
  })
});
const resultWithSender = await responseWithSender.json();
if (resultWithSender.success) {
  console.log('Balance data with custom sender:', resultWithSender.data);
} else {
  console.error('Error:', resultWithSender.error);
}
```

## Backend Integration

For backend applications in Python, you can use the simplified format without needing any Stacks-specific libraries:

```python
import requests
import json

def get_proposal(proposal_id, network='testnet', bust_cache=False):
    """
    Fetch a proposal from the contract using the cache service.
    
    Args:
        proposal_id (int): The ID of the proposal to fetch
        network (str): The Stacks network to use ('mainnet' or 'testnet')
        bust_cache (bool): Whether to bypass the cache and force a fresh request
        
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
        ],
        "network": network,
        "cacheControl": {
            "bustCache": bust_cache
        }
    }
    
    response = requests.post(
        url,
        headers={'Content-Type': 'application/json'},
        data=json.dumps(payload)
    )
    
    # Raise an exception for HTTP errors
    response.raise_for_status()
    
    result = response.json()
    if result.get('success'):
        return result['data']
    else:
        error = result.get('error', {})
        raise Exception(f"API Error: {error.get('code')} - {error.get('message')}")

def get_token_balance(address, token_contract_address, token_contract_name, network='mainnet', 
                     custom_ttl=None, bust_cache=False, skip_cache=False, sender_address=None):
    """
    Fetch a token balance for an address.
    
    Args:
        address (str): The Stacks address to check
        token_contract_address (str): The contract address of the token
        token_contract_name (str): The contract name of the token
        network (str): The Stacks network to use ('mainnet' or 'testnet')
        custom_ttl (int, optional): Custom cache TTL in seconds
        bust_cache (bool): Whether to bypass the cache and force a fresh request
        skip_cache (bool): Whether to skip caching this result
        sender_address (str, optional): Optional sender address for the contract call
        
    Returns:
        dict: The balance data
    """
    url = f'https://cache.aibtc.dev/contract-calls/read-only/{token_contract_address}/{token_contract_name}/get-balance'
    
    # Build the payload with cache control options if needed
    payload = {
        "functionArgs": [
            {
                "type": "principal",
                "value": address
            }
        ],
        "network": network
    }
    
    # Add sender address if specified
    if sender_address:
        payload["senderAddress"] = sender_address
    
    # Add cache control options if any are specified
    cache_control = {}
    if custom_ttl is not None:
        cache_control["ttl"] = custom_ttl
    if bust_cache:
        cache_control["bustCache"] = True
    if skip_cache:
        cache_control["skipCache"] = True
        
    if cache_control:
        payload["cacheControl"] = cache_control
    
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

# Usage examples
if __name__ == "__main__":
    try:
        # Get proposal with ID 3 from testnet
        proposal = get_proposal(3, network='testnet')
        print(f"Proposal data: {json.dumps(proposal, indent=2)}")
        
        # Get fresh proposal data (bypass cache)
        fresh_proposal = get_proposal(3, network='testnet', bust_cache=True)
        print(f"Fresh proposal data: {json.dumps(fresh_proposal, indent=2)}")
        
        # Get token balance for an address on mainnet with custom TTL
        balance = get_token_balance(
            "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
            "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
            "media3-token",
            network='mainnet',
            custom_ttl=600  # Cache for 10 minutes
        )
        print(f"Token balance: {balance}")
        
        # Example of skipping cache for a frequently changing value
        latest_price = get_token_balance(
            "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
            "SP2C2YFP12AJZB4MABJBAJ55XECVS7E4PMMZ89YZR",
            "usda-token",
            network='mainnet',
            custom_ttl=0  # Don't cache this result
        )
        print(f"Latest price: {latest_price}")
        
    except Exception as e:
        print(f"Error: {e}")
```

## Error Handling Examples

### JavaScript Error Handling

```javascript
async function callContract(contractAddress, contractName, functionName, args) {
  try {
    const response = await fetch(
      `https://cache.aibtc.dev/contract-calls/read-only/${contractAddress}/${contractName}/${functionName}`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          functionArgs: args
        })
      }
    );
    
    const result = await response.json();
    
    if (result.success) {
      return result.data;
    } else {
      // Handle specific error codes
      switch (result.error.code) {
        case 'INVALID_CONTRACT_ADDRESS':
          console.error('The contract address is invalid:', result.error.details.address);
          break;
        case 'INVALID_FUNCTION':
          console.error(`Function ${result.error.details.function} not found in contract`);
          break;
        case 'INVALID_ARGUMENTS':
          console.error(`Invalid arguments: ${result.error.details.reason}`);
          break;
        case 'INVALID_NETWORK':
          console.error(`Invalid network: ${result.error.details.network}`);
          break;
        case 'UPSTREAM_API_ERROR':
          console.error('Error from Stacks API:', result.error.message);
          // Check if we should retry based on the error
          if (result.error.details.retryable) {
            console.log(`This error is retryable. Retry after ${result.error.details.retryAfter || '1s'}`);
          }
          break;
        case 'RATE_LIMIT_EXCEEDED':
          console.error('Rate limit exceeded. Try again later.');
          console.log(`Retry after: ${result.error.details.retryAfter || '60s'}`);
          break;
        case 'TIMEOUT':
          console.error('The request timed out. The network might be congested.');
          break;
        default:
          console.error(`Error: ${result.error.code} - ${result.error.message}`);
      }
      
      throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
    }
  } catch (error) {
    // Handle network errors or other exceptions
    console.error('Failed to call contract:', error);
    throw error;
  }
}
```

### Python Error Handling

```python
import requests
import json

class ApiError(Exception):
    def __init__(self, code, message, details=None, error_id=None):
        self.code = code
        self.message = message
        self.details = details or {}
        self.error_id = error_id
        super().__init__(f"{code}: {message}")

def call_contract(contract_address, contract_name, function_name, args):
    """
    Call a read-only contract function with error handling
    
    Args:
        contract_address (str): The contract address
        contract_name (str): The contract name
        function_name (str): The function to call
        args (list): The function arguments
        
    Returns:
        The function result
        
    Raises:
        ApiError: If the API returns an error
        requests.RequestException: For network-related errors
    """
    url = f'https://cache.aibtc.dev/contract-calls/read-only/{contract_address}/{contract_name}/{function_name}'
    
    payload = {
        "functionArgs": args
    }
    
    try:
        response = requests.post(
            url,
            headers={'Content-Type': 'application/json'},
            data=json.dumps(payload)
        )
        
        # Raise HTTP errors
        response.raise_for_status()
        
        result = response.json()
        
        if result.get('success'):
            return result['data']
        else:
            error = result.get('error', {})
            raise ApiError(
                code=error.get('code', 'UNKNOWN_ERROR'),
                message=error.get('message', 'Unknown error occurred'),
                details=error.get('details'),
                error_id=error.get('id')
            )
            
    except requests.exceptions.RequestException as e:
        print(f"Network error: {e}")
        raise
        
# Usage example with error handling
try:
    result = call_contract(
        "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
        "media3-action-proposals-v2",
        "get-proposal",
        [{"type": "uint", "value": "3"}]
    )
    print(f"Success: {json.dumps(result, indent=2)}")
    
except ApiError as e:
    print(f"API Error ({e.code}): {e.message}")
    if e.details:
        print(f"Details: {json.dumps(e.details, indent=2)}")
    if e.error_id:
        print(f"Error ID: {e.error_id}")
        
except requests.exceptions.RequestException as e:
    print(f"Network error: {e}")
    
except Exception as e:
    print(f"Unexpected error: {e}")
```
