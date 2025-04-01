# Cache Services

The AIBTC Cache system includes several service classes that handle different aspects of caching, rate limiting, and API interactions. These services are used internally by the Durable Objects to provide efficient and reliable access to external data.

## KV Cache Service

The `CacheService` provides a simple interface for caching data in Cloudflare KV storage.

### Features

- JSON serialization/deserialization with BigInt support
- Configurable TTL (Time-To-Live) with default value
- Option to cache items indefinitely (no expiration)
- Special handling for legacy BigInt values with 'n' suffix
- Comprehensive error handling with standardized ApiError responses
- Detailed logging for cache operations

### Methods

- `get<T>(key: string): Promise<T | null>` - Retrieves a value from the cache, returns null if not found
- `set(key: string, value: unknown, ttl?: number): Promise<void>` - Stores a value in the cache with optional TTL

### How It Works

The cache service operates as follows:

1. When storing a value, it serializes the data to JSON with special handling for BigInt values
2. TTL can be specified per item, defaulting to the service's configured default TTL
3. Setting TTL to 0 or enabling ignoreTtl will cache items indefinitely
4. When retrieving a value, it handles parsing with special consideration for legacy BigInt formats
5. All operations are logged, with errors being captured in a standardized format
6. Cache errors are wrapped in ApiError with the ErrorCode.CACHE_ERROR code

## Token Bucket Service

The `TokenBucket` implements a token bucket algorithm for rate limiting.

### Features

- Automatic token refilling over time based on elapsed time
- Configurable bucket size and refill rate
- Thread-safe token consumption
- Efficient token calculation that only happens when tokens are requested

### Methods

- `getToken(): boolean` - Attempts to get a token from the bucket (returns true if a token was available and consumed)
- `getAvailableTokens(): number` - Gets the current number of available tokens after refilling based on elapsed time

### How It Works

The token bucket algorithm works by:

1. Starting with a full bucket of tokens (maxTokens)
2. Calculating a refill rate based on maxTokens / refillIntervalMs
3. When tokens are requested, automatically refilling the bucket based on elapsed time since the last refill
4. Only allowing requests when tokens are available
5. Consuming one token per request

This provides a smooth rate limiting mechanism that allows for bursts of traffic up to the bucket size, while maintaining a consistent average rate over time.

## Request Queue Service

The `RequestQueue<T>` manages a queue of requests with rate limiting and automatic retries.

### Features

- Rate limiting using the token bucket algorithm
- Automatic retries with exponential backoff for failed requests
- Minimum request spacing to prevent bursts (at least 250ms between requests)
- Comprehensive error handling and logging with request IDs for tracking
- Request timeout protection to prevent hanging requests
- Queue time tracking to monitor performance

### Methods

- `enqueue(execute: () => Promise<T>): Promise<T>` - Adds a request to the queue and returns a promise that resolves when the request completes
- `getQueueLength(): number` - Returns the current length of the request queue

### How It Works

The request queue processes requests as follows:

1. When a request is enqueued, it's added to the queue with a unique request ID
2. The queue processor checks if a token is available from the rate limiter
3. If a token is available, it processes the next request in the queue
4. It ensures minimum spacing between requests to prevent API overload
5. If a request fails, it's retried with exponential backoff (delay doubles with each retry)
6. Detailed metrics are logged, including queue time, execution time, and retry attempts
7. Requests can be wrapped with timeouts to prevent hanging operations

## API Rate Limiter Service

The `ApiRateLimiterService` provides rate-limited API fetching capabilities.

### Features

- Caching of API responses with configurable TTL
- Request queuing and rate limiting using token bucket algorithm
- Automatic retries for failed requests with exponential backoff
- Standardized success/error response format with detailed error information
- Performance tracking and logging for monitoring

### Methods

- `fetch(endpoint: string, cacheKey: string, bustCache?: boolean): Promise<Response>` - Fetches data from an API endpoint
- `getQueueLength(): number` - Returns the current length of the request queue
- `getTokenCount(): number` - Returns the current number of available tokens
- `getWindowRequestsCount(): number` - Returns the number of requests made in the current time window

## Performance Tracking

The AIBTC Cache includes comprehensive performance tracking to monitor and optimize the system:

### Request Duration Tracking

All requests are timed and logged with the following thresholds:

- **Normal**: Under 1000ms (1 second)
- **Slow**: 1000-2000ms (1-2 seconds)
- **Very Slow**: Over 2000ms (2+ seconds)

Slow and very slow requests are logged with additional context to help identify bottlenecks.

### Queue Time Tracking

For queued requests, the system tracks:

- Time spent in queue before processing
- Total time (queue time + execution time)
- Queue position when the request was enqueued

### Performance Logging

Performance metrics are logged with the following information:

- Request ID for correlation
- Duration in milliseconds
- Queue time (if applicable)
- Cache hit/miss status
- Endpoint or contract call details

### Slow Request Handling

When a request exceeds the slow threshold:

1. A warning is logged with detailed context
2. The request continues to be processed normally
3. If the same endpoint consistently produces slow responses, it may indicate an issue with the upstream API

### Performance Optimization Tips

To get the best performance from the cache:

1. Use consistent cache keys for the same data
2. Batch related requests when possible
3. Use appropriate TTL values based on data volatility
4. Monitor for slow requests in your application logs
5. Consider implementing client-side caching for frequently accessed data
- `getPerformanceStats(): { avgResponseTime: number, slowestRequests: Array<{ endpoint: string, time: number }> }` - Returns performance statistics for API requests

## Stacks API Service

The `StacksApiService` provides methods for interacting with the Stacks blockchain API.

### Features

- Performance tracking for slow contract calls
- Comprehensive error handling with ApiError
- Detailed logging

### Methods

- `callReadOnlyFunction(contractAddress: string, contractName: string, functionName: string, functionArgs: any[], senderAddress: string, network: StacksNetworkName): Promise<ClarityValue>` - Calls a read-only function on a Stacks smart contract

## Stacks Contract Fetcher

The `StacksContractFetcher` handles fetching data from Stacks smart contracts with caching and rate limiting.

### Features

- Caching of contract call responses with configurable TTL
- Rate limiting and request queuing to prevent API overload
- Automatic retries for failed requests with exponential backoff
- Network validation ('mainnet' or 'testnet')
- Configurable request timeouts to prevent hanging operations
- Fine-grained cache control (bustCache, skipCache, custom TTL)

### Methods

- `fetch(contractAddress: string, contractName: string, functionName: string, functionArgs: any[], senderAddress: string, network: string, cacheKey: string, bustCache?: boolean, skipCache?: boolean, ttl?: number): Promise<ClarityValue>` - Fetches data from a Stacks smart contract with caching and rate limiting

### How It Works

The contract fetcher operates as follows:

1. First checks the cache using the provided cacheKey (unless bustCache is true)
2. Validates the network parameter ('mainnet' or 'testnet')
3. Queues the request through the RequestQueue service, which handles rate limiting
4. Makes the actual contract call through the StacksApiService
5. Caches the result with the specified TTL (unless skipCache is true)
6. Returns the Clarity value from the contract call

This layered approach ensures efficient use of the Stacks API while providing reliable access to contract data.

## Contract ABI Service

The `ContractAbiService` handles fetching and managing Clarity smart contract ABIs.

### Features

- Caching of contract ABIs indefinitely (since contract code never changes after deployment)
- Validation of function calls against ABIs to ensure compatibility
- Validation of function arguments against ABI specifications
- Tracking of known contracts for monitoring and statistics
- Stacks address validation to prevent invalid requests
- Network detection based on address prefixes (SP/SM for mainnet, ST/SN for testnet)

### Methods

- `fetchContractABI(contractAddress: string, contractName: string, bustCache?: boolean): Promise<ClarityAbi>` - Fetches a contract's ABI and caches it indefinitely
- `validateFunctionInABI(abi: ClarityAbi, functionName: string): boolean` - Validates if a function exists in the contract ABI
- `validateFunctionArgs(abi: ClarityAbi, functionName: string, functionArgs: any[]): { valid: boolean; error?: string }` - Validates function arguments against the ABI specification
- `getKnownContracts(): Promise<{ stats: { total: number; cached: number }; contracts: { cached: Array<{ contractAddress: string; contractName: string }> } }>` - Gets the list of known contracts that have been cached

### How It Works

The contract ABI service operates as follows:

1. When an ABI is requested, it first validates the contract address format
2. It checks the cache for the ABI using a consistent key format
3. If not found (or bustCache is true), it determines the network from the address prefix
4. It fetches the ABI from the Stacks API using the @stacks/transactions library
5. The ABI is cached indefinitely since contract code never changes after deployment
6. The contract is added to the list of known contracts for tracking
7. The service provides methods to validate function calls and arguments against the ABI
8. For function validation, it checks if the function exists and has the correct access type
9. For argument validation, it checks count and types against the ABI specification

## Cache Key Service

The `CacheKeyService` generates deterministic cache keys for contract calls.

### Features

- Consistent key generation for identical contract calls
- Hashing of function arguments to keep key length reasonable
- Special handling for BigInt and Buffer serialization
- Configurable prefix for organizational purposes

### Methods

- `generateContractCallKey(contractAddress: string, contractName: string, functionName: string, functionArgs: ClarityValue[], network: string): string` - Generates a deterministic cache key for a contract call

### How It Works

The cache key service operates as follows:

1. It serializes function arguments to a stable string representation
2. Special handling is provided for BigInt values and Buffers
3. A hash of the arguments is created to keep the key length reasonable
4. The key combines contract address, contract name, function name, network, and the argument hash
5. This ensures that identical calls produce the same cache key for better cache hit rates
6. The deterministic nature allows different clients to benefit from the same cached values
