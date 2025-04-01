# Available Endpoints

| Endpoint                                        | Description                                      |
| ----------------------------------------------- | ------------------------------------------------ |
| [Decode Clarity Value](decode-clarity-value.md) | Decode Clarity values into JavaScript/JSON       |
| [Read-Only Function Calls](read-only-calls.md)  | Make read-only calls to smart contract functions |
| [Contract ABI](contract-abi.md)                 | Retrieve the ABI for a smart contract            |
| [Known Contracts](known-contracts.md)           | List all contracts accessed through the cache    |

## Rate Limiting

All endpoints that make calls to the Stacks API are rate-limited to protect both our service and the upstream Stacks API. The current limits are:

- Maximum of 20 requests per minute to the Stacks API
- Minimum spacing of 250ms between consecutive requests
- Automatic queuing of requests that exceed these limits

When rate limits are exceeded, requests are automatically queued and processed as capacity becomes available. For high-volume applications, we recommend implementing client-side caching to reduce the number of requests.

## Response Times

Expected response times vary by endpoint:

- **Decode Clarity Value**: < 100ms (processed locally)
- **Contract ABI**: 
  - First request: 500-1500ms (fetched from Stacks API)
  - Subsequent requests: < 100ms (served from cache)
- **Read-Only Function Calls**:
  - Cached responses: < 100ms
  - Uncached simple calls: 500-1500ms
  - Complex contract calls: 1-5 seconds
- **Known Contracts**: < 100ms (processed locally)

All endpoints have a maximum timeout of 5 seconds for upstream API calls.
