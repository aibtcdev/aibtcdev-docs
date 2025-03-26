---
description: Tools for interacting with Smart Wallets
---

# Smart Wallet Tools

Smart Wallet tools provide functionality for deploying, managing, and interacting with Smart Wallets, which are programmable wallets that can hold assets and interact with various contracts on the Stacks blockchain.

## Tool Overview

| Tool Name | Description | Key Features |
|-----------|-------------|--------------|
| `smartwallet_deploy_smart_wallet` | Deploy a new smart wallet | Owner assignment, DAO token linking |
| `smartwallet_deposit_stx` | Deposit STX to a smart wallet | Transaction creation, balance update |
| `smartwallet_deposit_ft` | Deposit fungible tokens to a smart wallet | Token transfers, balance update |
| `smartwallet_approve_asset` | Approve an asset for use with the smart wallet | Asset authorization |
| `smartwallet_revoke_asset` | Revoke an asset from the smart wallet | Asset deauthorization |
| `smartwallet_get_balance_stx` | Get the STX balance from a smart wallet | Current balance |
| `smartwallet_is_approved_asset` | Check if an asset is approved in the smart wallet | Asset status |
| `smartwallet_get_configuration` | Get the configuration of a smart wallet | Comprehensive wallet info |

## Tool Details

### smartwallet_deploy_smart_wallet

Deploys a new smart wallet for a user.

**Input Parameters**:
- `owner_address`: Stacks address of the wallet owner
- `dao_token_contract`: Contract principal of the DAO token

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "smart_wallet_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18",
  "owner": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM"
}
```

**Example Prompt**:
```
Deploy a new smart wallet with the following details:
- owner_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
- dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
```

### smartwallet_deposit_stx

Deposits STX into a smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `amount`: Amount of STX to deposit in microstacks

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 1000000,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Deposit STX to a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
- amount: 1000000
```

### smartwallet_deposit_ft

Deposits fungible tokens into a smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `ft_contract`: Contract principal of the fungible token
- `amount`: Amount of tokens to deposit

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 100,
  "token_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Deposit fungible tokens to a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
- ft_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
- amount: 100
```

### smartwallet_approve_asset

Approves an asset for use with the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `asset_contract`: Contract principal of the asset to approve

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Approve an asset for use with the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory
```

### smartwallet_revoke_asset

Revokes an asset from the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `asset_contract`: Contract principal of the asset to revoke

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Revoke an asset from the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory
```

### smartwallet_get_balance_stx

Gets the STX balance from a smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet

**Output**:
```json
{
  "balance": 1000000,
  "readable": "1.0 STX",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Get the STX balance from a smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
```

### smartwallet_is_approved_asset

Checks if a specific asset is approved in the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `asset_contract`: Contract principal of the asset to check

**Output**:
```json
{
  "approved": true,
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18"
}
```

**Example Prompt**:
```
Check if an asset is approved in the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory
```

### smartwallet_get_configuration

Gets the configuration of a smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet

**Output**:
```json
{
  "owner": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "dao_token": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "sbtc_token": "STV9K21TBFAK4KNRJXF5DFP8N7W46G4V9RJ5XDY2.sbtc-token",
  "approved_assets": [
    "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory"
  ],
  "created_at": 12345
}
```

**Example Prompt**:
```
Get the configuration of a smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
```

## Smart Wallet Workflow Example

Here's a complete workflow for deploying and using a smart wallet:

1. **Deploy a new smart wallet**
   ```
   Deploy a new smart wallet with the following details:
   - owner_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
   - dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   ```

2. **Deposit STX to the smart wallet**
   ```
   Deposit STX to my smart wallet with the following details:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
   - amount: 1000000
   ```

3. **Approve an asset for use with the smart wallet**
   ```
   Approve the Faktory DEX for use with my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory
   ```

4. **Check if an asset is approved**
   ```
   Check if the Faktory DEX is approved for my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory
   ```

5. **Get the smart wallet configuration**
   ```
   Get the configuration of my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST3YT-S5D18
   ```

## Error Handling

All Smart Wallet tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Unauthorized access",
  "code": 8001
}
```

Common error codes:
- 8001: Unauthorized access
- 8002: Asset not found
- 8003: Insufficient balance
- 8004: Smart wallet not found
- 8005: Asset already approved
