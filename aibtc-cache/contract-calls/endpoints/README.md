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

## Request Queuing

The AIBTC Cache implements automatic request queuing to handle high traffic volumes while maintaining fair access to the Stacks API.

### How Queuing Works

1. When a request arrives, it's assigned a unique request ID
2. If capacity is available, the request is processed immediately
3. If capacity is not available, the request enters a queue
4. Requests are processed in FIFO (First In, First Out) order
5. Queue status is tracked and logged for monitoring

### Queue Metrics

The following metrics are tracked for each request:

- Queue position when the request was enqueued
- Time spent in queue before processing
- Total request time (queue time + processing time)

### Queue Behavior During High Load

During periods of high load:

- Requests are automatically queued
- Each request is processed when capacity becomes available
- Responses include the total processing time
- No requests are dropped unless they time out

### Client Recommendations

For optimal performance during high load:

- Implement client-side timeouts appropriate for your use case
- Consider exponential backoff for retries
- Use the cache control options to reduce unnecessary requests
- Batch related requests when possible
