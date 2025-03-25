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
// import { clarity as cl } from '@stacks/transactions';

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

For backend applications, you can use either Stacks.js Clarity values or the simplified format:

```javascript
// Node.js example using fetch and @stacks/transactions
const fetch = require('node-fetch');
const { uintCV } = require('@stacks/transactions');
// Or using the clarity namespace
// const { clarity: cl } = require('@stacks/transactions');

// Using Stacks.js Clarity values directly
async function getProposalWithStacksJs(id) {
  const response = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      functionArgs: [uintCV(id)]  // Use Stacks.js Clarity values directly
      // Or with clarity namespace: [cl.uint(id)]
    })
  });
  
  return response.json();
}

// Using simplified format (no Stacks.js dependency required)
async function getProposalSimplified(id) {
  const response = await fetch('https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      functionArgs: [
        {
          type: 'uint',
          value: id.toString()
        }
      ]
    })
  });
  
  return response.json();
}

// Usage
getProposalWithStacksJs(3).then(proposal => console.log(proposal));
getProposalSimplified(3).then(proposal => console.log(proposal));
```
