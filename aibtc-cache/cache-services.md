# Cache Services

The AIBTC Cache system includes several service classes that handle different aspects of caching, rate limiting, and API interactions. These services are used internally by the Durable Objects to provide efficient and reliable access to external data.

## KV Cache Service

The `CacheService` provides a simple interface for caching data in Cloudflare KV storage.

### Features

- JSON serialization/deserialization with BigInt support
- Configurable TTL (Time-To-Live)
- Option to cache items indefinitely

### Methods

- `get<T>(key: string): Promise<T | null>` - Retrieves a value from the cache
- `set(key: string, value: unknown, ttl?: number): Promise<void>` - Stores a value in the cache

## Token Bucket Service

The `TokenBucket` implements a token bucket algorithm for rate limiting.

### Features

- Automatic token refilling over time
- Configurable bucket size and refill rate
- Thread-safe token consumption

### Methods

- `getToken(): boolean` - Attempts to get a token from the bucket
- `getAvailableTokens(): number` - Gets the current number of available tokens

## Request Queue Service

The `RequestQueue<T>` manages a queue of requests with rate limiting and automatic retries.

### Features

- Rate limiting using the token bucket algorithm
- Automatic retries with exponential backoff
- Minimum request spacing to prevent bursts

### Methods

- `enqueue(execute: () => Promise<T>): Promise<T>` - Adds a request to the queue
- `getQueueLength(): number` - Returns the current length of the queue

## API Rate Limiter Service

The `ApiRateLimiterService` provides rate-limited API fetching capabilities.

### Features

- Caching of API responses
- Request queuing and rate limiting
- Automatic retries for failed requests

### Methods

- `fetch(endpoint: string, cacheKey: string, bustCache?: boolean): Promise<Response>` - Fetches data from an API endpoint
- `getQueueLength(): number` - Returns the current length of the request queue
- `getTokenCount(): number` - Returns the current number of available tokens
- `getWindowRequestsCount(): number` - Returns the number of requests made in the current time window

## Stacks API Service

The `StacksApiService` provides methods for interacting with the Stacks blockchain API.

### Methods

- `callReadOnlyFunction(contractAddress: string, contractName: string, functionName: string, functionArgs: any[], senderAddress: string, network: StacksNetworkName): Promise<ClarityValue>` - Calls a read-only function on a Stacks smart contract

## Stacks Contract Fetcher

The `StacksContractFetcher` handles fetching data from Stacks smart contracts with caching and rate limiting.

### Features

- Caching of contract call responses
- Rate limiting and request queuing
- Automatic retries for failed requests

### Methods

- `fetch(contractAddress: string, contractName: string, functionName: string, functionArgs: any[], senderAddress: string, network: string, cacheKey: string, bustCache?: boolean): Promise<ClarityValue>` - Fetches data from a Stacks smart contract

## Contract ABI Service

The `ContractAbiService` handles fetching and managing Clarity smart contract ABIs.

### Features

- Caching of contract ABIs (indefinitely, as they don't change)
- Validation of function calls against ABIs
- Tracking of known contracts

### Methods

- `fetchContractABI(contractAddress: string, contractName: string, bustCache?: boolean): Promise<ClarityAbi>` - Fetches a contract's ABI
- `validateFunctionInABI(abi: ClarityAbi, functionName: string): boolean` - Validates if a function exists in the contract ABI
- `validateFunctionArgs(abi: ClarityAbi, functionName: string, functionArgs: any[]): { valid: boolean; error?: string }` - Validates function arguments against the ABI specification
- `getKnownContracts(): Promise<{ stats: { total: number; cached: number }; contracts: { cached: Array<{ contractAddress: string; contractName: string }> } }>` - Gets the list of known contracts
