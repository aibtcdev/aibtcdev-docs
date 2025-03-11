---
description: Tools for managing cryptocurrency wallets
---

# Wallet Tools

Wallet tools provide functionality for managing cryptocurrency wallets, checking balances, sending transactions, and retrieving wallet information.

## Tool Overview

| Tool Name | Description | Key Features |
|-----------|-------------|--------------|
| `wallet_get_my_balance` | Get the STX balance of the agent's wallet | Current balance, readable format |
| `wallet_get_my_address` | Get the address of the agent's wallet | Principal format, readable format |
| `wallet_fund_my_wallet_faucet` | Request testnet STX from the faucet | Automatic funding, status tracking |
| `wallet_send_stx` | Send STX to another address | Transaction creation, fee estimation |
| `wallet_get_my_transactions` | Get transaction history | Filtering, pagination, detailed info |
| `wallet_send_sip10` | Send SIP-10 tokens to another address | Token transfers, fee estimation |

## Tool Details

### wallet_get_my_balance

Retrieves the current STX balance of the agent's wallet.

**Input Parameters**: None

**Output**:
```json
{
  "balance": "1000000",
  "readable": "1.0 STX"
}
```

**Example Usage**:
```
Use the wallet_get_my_balance tool to check my current STX balance
```

### wallet_get_my_address

Retrieves the Stacks address (principal) of the agent's wallet.

**Input Parameters**: None

**Output**:
```json
{
  "address": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "readable": "ST1PQHQ...ZPGZGM"
}
```

**Example Usage**:
```
Use the wallet_get_my_address tool to get my wallet address
```

### wallet_fund_my_wallet_faucet

Requests testnet STX from the faucet to fund the agent's wallet.

**Input Parameters**: None

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "message": "Faucet request successful. Funds will arrive shortly."
}
```

**Example Usage**:
```
Use the wallet_fund_my_wallet_faucet tool to get some testnet STX
```

### wallet_send_stx

Sends STX from the agent's wallet to another address.

**Input Parameters**:
- `amount`: Amount of STX to send (in microSTX)
- `recipient`: Recipient address
- `memo` (optional): Transaction memo

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "status": "pending"
}
```

**Example Usage**:
```
Use the wallet_send_stx tool with amount=1000000 (1 STX) and recipient=ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
```

### wallet_get_my_transactions

Retrieves transaction history for the agent's wallet.

**Input Parameters**:
- `limit` (optional): Number of transactions to return
- `offset` (optional): Pagination offset

**Output**:
```json
{
  "transactions": [
    {
      "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
      "status": "success",
      "type": "token_transfer",
      "amount": "1000000",
      "recipient": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
      "timestamp": 1678901234
    }
  ],
  "total": 10
}
```

**Example Usage**:
```
Use the wallet_get_my_transactions tool with limit=5 to see my recent transactions
```

### wallet_send_sip10

Sends SIP-10 tokens from the agent's wallet to another address.

**Input Parameters**:
- `amount`: Amount of tokens to send
- `recipient`: Recipient address
- `token_contract`: Contract address of the token
- `memo` (optional): Transaction memo

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "status": "pending"
}
```

**Example Usage**:
```
Use the wallet_send_sip10 tool with amount=10, recipient=ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM, and token_contract=ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token
```

## Error Handling

All wallet tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Insufficient balance",
  "code": 4001
}
```

Common error codes:
- 4001: Insufficient balance
- 4002: Invalid address
- 4003: Transaction failed
- 4004: Network error
