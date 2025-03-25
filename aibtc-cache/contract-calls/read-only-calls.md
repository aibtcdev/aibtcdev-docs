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

## Example Request (cURL)

```bash
curl -X POST \
  https://cache.aibtc.dev/contract-calls/read-only/ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA/media3-action-proposals-v2/get-proposal \
  -H "Content-Type: application/json" \
  -d '{"functionArgs": [{ "type": "uint", "value": "3" }]}' \
  -w "\n"
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
