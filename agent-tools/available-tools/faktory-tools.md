---
description: Tools for interacting with Faktory DEX
---

# Faktory Tools

Faktory tools provide functionality for interacting with the Faktory DEX, including buying and selling tokens, getting quotes, and retrieving token information.

## Tool Overview

| Tool Name | Description | Key Features |
|-----------|-------------|--------------|
| `faktory_get_sbtc` | Request testnet sBTC from the faucet | Automatic funding |
| `faktory_exec_buy` | Execute a buy order with BTC | Order execution, slippage control |
| `faktory_exec_buy_stx` | Execute a buy order with STX | Order execution, slippage control |
| `faktory_exec_sell` | Execute a sell order | Order execution, slippage control |
| `faktory_get_dao_tokens` | Get a list of DAO tokens | Pagination, search, sorting |
| `faktory_get_token` | Get detailed information about a token | Price, volume, market data |

## Tool Details

### faktory_get_sbtc

Requests testnet sBTC from the Faktory faucet.

**Input Parameters**: None

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "message": "sBTC request successful. Funds will arrive shortly."
}
```

**Example Prompt**:
```
Request testnet sBTC from the Faktory faucet.
```

### faktory_exec_buy

Executes a buy order on Faktory DEX using BTC.

**Input Parameters**:
- `btc_amount`: Amount of BTC to spend (e.g., "0.0004")
- `dao_token_dex_contract_address`: Contract address of the token on DEX
- `slippage` (optional): Slippage tolerance in basis points (default: "15")

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount_spent": "0.0004",
  "tokens_received": "100",
  "price_per_token": "0.000004"
}
```

**Example Prompt**:
```
Execute a buy order for tokens on the Faktory DEX with the following details:
- btc_amount: 0.0004
- dao_token_dex_contract_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token
```

### faktory_exec_buy_stx

Executes a buy order on Faktory DEX using STX.

**Input Parameters**:
- `stx_amount`: Amount of STX to spend (e.g., "100")
- `dao_token_dex_contract_address`: Contract address of the token on DEX
- `slippage` (optional): Slippage tolerance in percentage (default: "15")

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount_spent": "100",
  "tokens_received": "500",
  "price_per_token": "0.2"
}
```

**Example Prompt**:
```
Execute a buy order with STX on the Faktory DEX with the following details:
- stx_amount: 100
- dao_token_dex_contract_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token
```

### faktory_exec_sell

Executes a sell order on Faktory DEX.

**Input Parameters**:
- `token_amount`: Amount of tokens to sell (e.g., "100")
- `dao_token_dex_contract_address`: Contract address of the token on DEX
- `slippage` (optional): Slippage tolerance in percentage (default: "15")

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount_sold": "100",
  "btc_received": "0.0004",
  "price_per_token": "0.000004"
}
```

**Example Prompt**:
```
Execute a sell order on the Faktory DEX with the following details:
- token_amount: 100
- dao_token_dex_contract_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token
```

### faktory_get_dao_tokens

Retrieves a list of DAO tokens from Faktory.

**Input Parameters**:
- `page` (optional): Page number for pagination (default: "1")
- `limit` (optional): Number of items per page (default: "10")
- `search` (optional): Search term to filter tokens
- `sort_order` (optional): Sort order for the results

**Output**:
```json
{
  "tokens": [
    {
      "name": "My DAO Token",
      "symbol": "MDT",
      "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token",
      "dex_contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token-dex",
      "price_btc": "0.000004",
      "price_stx": "0.2",
      "market_cap": "1000000",
      "volume_24h": "50000"
    }
  ],
  "total": 100,
  "page": 1,
  "limit": 10
}
```

**Example Prompt**:
```
Get a list of DAO tokens from Faktory with the following criteria:
- limit: 5
- search: bitcoin
```

### faktory_get_token

Retrieves detailed information about a token from its DEX contract.

**Input Parameters**:
- `dex_contract_id`: Contract ID of the DEX

**Output**:
```json
{
  "name": "My DAO Token",
  "symbol": "MDT",
  "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token",
  "dex_contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token-dex",
  "price_btc": "0.000004",
  "price_stx": "0.2",
  "market_cap": "1000000",
  "volume_24h": "50000",
  "total_supply": "5000000",
  "circulating_supply": "2500000",
  "holders": 150,
  "liquidity": {
    "btc": "10",
    "token": "2500000"
  }
}
```

**Example Prompt**:
```
Get detailed information about a token from its DEX contract.
- dex_contract_id: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token-dex
```

## Error Handling

All Faktory tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Insufficient balance",
  "code": 6001
}
```

Common error codes:
- 6001: Insufficient balance
- 6002: Slippage too high
- 6003: Token not found
- 6004: Liquidity too low
- 6005: Transaction failed
