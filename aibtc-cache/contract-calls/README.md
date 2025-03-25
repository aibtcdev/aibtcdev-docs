# Contract Calls Endpoints

The Contract Calls Durable Object provides a caching layer for interacting with Stacks smart contracts. It allows you to make read-only function calls to any Stacks smart contract while benefiting from caching, rate limiting, and automatic retries.

## Base Path

All contract call endpoints are available under:
```
/contract-calls
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| [Read-Only Function Calls](read-only-calls.md) | Make read-only calls to smart contract functions |
| [Contract ABI](contract-abi.md) | Retrieve the ABI for a smart contract |
| [Known Contracts](known-contracts.md) | List all contracts accessed through the cache |
| [Decode Clarity Value](decode-clarity-value.md) | Decode Clarity values into JavaScript/JSON |
| [Clarity Value Types](clarity-value-types.md) | Reference for Clarity value types |
| [Integration Examples](integration-examples.md) | Examples for frontend and backend integration |
