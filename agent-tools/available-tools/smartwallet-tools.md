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
| `smartwallet_withdraw_stx` | Withdraw STX from a smart wallet | Transaction creation, balance update |
| `smartwallet_deposit_ft` | Deposit fungible tokens to a smart wallet | Token transfers, balance update |
| `smartwallet_withdraw_ft` | Withdraw fungible tokens from a smart wallet | Token transfers, balance update |
| `smartwallet_approve_asset` | Approve an asset for use with the smart wallet | Asset authorization |
| `smartwallet_revoke_asset` | Revoke an asset from the smart wallet | Asset deauthorization |
| `smartwallet_approve_dex` | Approve a DEX for use with the smart wallet | DEX authorization |
| `smartwallet_revoke_dex` | Revoke a DEX from the smart wallet | DEX deauthorization |
| `smartwallet_set_agent_can_buy_sell` | Set whether agent can buy/sell assets | Permission management |
| `smartwallet_buy_asset` | Buy an asset from a DEX | Trading functionality |
| `smartwallet_sell_asset` | Sell an asset to a DEX | Trading functionality |
| `smartwallet_proxy_propose_action` | Propose an action to a DAO | Governance participation |
| `smartwallet_proxy_create_proposal` | Create a proposal in a DAO | Governance participation |
| `smartwallet_vote_on_action_proposal` | Vote on an action proposal | Governance participation |
| `smartwallet_vote_on_core_proposal` | Vote on a core proposal | Governance participation |
| `smartwallet_conclude_action_proposal` | Conclude an action proposal | Governance participation |
| `smartwallet_conclude_core_proposal` | Conclude a core proposal | Governance participation |
| `smartwallet_get_balance_stx` | Get the STX balance from a smart wallet | Current balance |
| `smartwallet_is_approved_asset` | Check if an asset is approved in the smart wallet | Asset status |
| `smartwallet_is_approved_dex` | Check if a DEX is approved in the smart wallet | DEX status |
| `smartwallet_get_configuration` | Get the configuration of a smart wallet | Comprehensive wallet info |

## Tool Details

### smartwallet_deploy_smart_wallet

Deploys a new smart wallet for a user.

**Input Parameters**:
- `owner_address`: Stacks address of the wallet owner
- `agent_address`: Stacks address of the agent
- `dao_token_contract`: Contract principal of the DAO token
- `dao_token_dex_contract` (optional): Contract principal of the DAO token DEX

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "smart_wallet_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG",
  "owner": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "agent": "ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG"
}
```

**Example Prompt**:
```
Deploy a new smart wallet with the following details:
- owner_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
- agent_address: ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG
- dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
- dao_token_dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
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
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Deposit STX to a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- amount: 1000000
```

### smartwallet_withdraw_stx

Withdraws STX from a smart wallet. Only the owner can withdraw.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `amount`: Amount of STX to withdraw in microstacks

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 1000000,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Withdraw STX from a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
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
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Deposit fungible tokens to a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- ft_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
- amount: 100
```

### smartwallet_withdraw_ft

Withdraws fungible tokens from a smart wallet. Only the owner can withdraw.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `ft_contract`: Contract principal of the fungible token
- `amount`: Amount of tokens to withdraw

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 100,
  "token_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Withdraw fungible tokens from a smart wallet with the following details:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
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
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Approve an asset for use with the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
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
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Revoke an asset from the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
```

### smartwallet_approve_dex

Approves a DEX for use with the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `dex_contract`: Contract principal of the DEX to approve

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "dex_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Approve a DEX for use with the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
```

### smartwallet_revoke_dex

Revokes a DEX from the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `dex_contract`: Contract principal of the DEX to revoke

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "dex_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Revoke a DEX from the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
```

### smartwallet_set_agent_can_buy_sell

Sets whether the agent can buy/sell assets through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `can_buy_sell`: Boolean indicating whether the agent can buy/sell (true/false)

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "can_buy_sell": true,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Set whether the agent can buy/sell assets through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- can_buy_sell: true
```

### smartwallet_buy_asset

Buys an asset from a DEX through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `dex_contract`: Contract principal of the DEX
- `asset_contract`: Contract principal of the asset to buy
- `amount`: Amount of the asset to buy

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "dex_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex",
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "amount": 100,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Buy an asset from a DEX through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
- amount: 100
```

### smartwallet_sell_asset

Sells an asset to a DEX through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `dex_contract`: Contract principal of the DEX
- `asset_contract`: Contract principal of the asset to sell
- `amount`: Amount of the asset to sell

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "dex_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex",
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "amount": 100,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Sell an asset to a DEX through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
- amount: 100
```

### smartwallet_proxy_propose_action

Proposes an action to a DAO through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `action_proposals_contract`: Contract principal of the action proposals extension
- `action_contract`: Contract principal of the action to propose
- `parameters`: Parameters for the action (format depends on the action)

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "action_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2",
  "action_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-send-message",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Propose an action to a DAO through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- action_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2
- action_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-send-message
- parameters: "Hello, DAO!"
```

### smartwallet_proxy_create_proposal

Creates a proposal in a DAO through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `core_proposals_contract`: Contract principal of the core proposals extension
- `proposal_contract`: Contract principal of the proposal to create
- `dao_token_contract`: Contract principal of the DAO token

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "core_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2",
  "proposal_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Create a proposal in a DAO through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
- proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
- dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
```

### smartwallet_vote_on_action_proposal

Votes on an action proposal through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `action_proposals_contract`: Contract principal of the action proposals extension
- `proposal_id`: ID of the proposal to vote on
- `vote`: Boolean indicating vote (true for yes, false for no)

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "action_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2",
  "proposal_id": 123,
  "vote": true,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Vote on an action proposal through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- action_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2
- proposal_id: 123
- vote: true
```

### smartwallet_vote_on_core_proposal

Votes on a core proposal through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `core_proposals_contract`: Contract principal of the core proposals extension
- `proposal_contract`: Contract principal of the proposal
- `vote`: Boolean indicating vote (true for yes, false for no)

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "core_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2",
  "proposal_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension",
  "vote": true,
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Vote on a core proposal through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
- proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
- vote: true
```

### smartwallet_conclude_action_proposal

Concludes an action proposal through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `action_proposals_contract`: Contract principal of the action proposals extension
- `proposal_id`: ID of the proposal to conclude
- `action_contract`: Contract principal of the action

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "action_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2",
  "proposal_id": 123,
  "action_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-send-message",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Conclude an action proposal through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- action_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2
- proposal_id: 123
- action_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-send-message
```

### smartwallet_conclude_core_proposal

Concludes a core proposal through the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `core_proposals_contract`: Contract principal of the core proposals extension
- `proposal_contract`: Contract principal of the proposal
- `dao_token_contract`: Contract principal of the DAO token

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "core_proposals_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2",
  "proposal_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Conclude a core proposal through the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
- proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
- dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
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
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Get the STX balance from a smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
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
  "asset_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Check if an asset is approved in the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
```

### smartwallet_is_approved_dex

Checks if a specific DEX is approved in the smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet
- `dex_contract`: Contract principal of the DEX to check

**Output**:
```json
{
  "approved": true,
  "dex_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex",
  "smart_wallet": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG"
}
```

**Example Prompt**:
```
Check if a DEX is approved in the smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
- dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
```

### smartwallet_get_configuration

Gets the configuration of a smart wallet.

**Input Parameters**:
- `smart_wallet_contract`: Contract principal of the smart wallet

**Output**:
```json
{
  "owner": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "agent": "ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG",
  "dao_token": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token",
  "sbtc_token": "STV9K21TBFAK4KNRJXF5DFP8N7W46G4V9RJ5XDY2.sbtc-token",
  "approved_assets": [
    "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token"
  ],
  "approved_dexes": [
    "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex"
  ],
  "agent_can_buy_sell": true,
  "created_at": 12345
}
```

**Example Prompt**:
```
Get the configuration of a smart wallet:
- smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
```

## Smart Wallet Workflow Examples

### Asset Management Workflow

1. **Deploy a new smart wallet**
   ```
   Deploy a new smart wallet with the following details:
   - owner_address: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
   - agent_address: ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG
   - dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   - dao_token_dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
   ```

2. **Deposit STX to the smart wallet**
   ```
   Deposit STX to my smart wallet with the following details:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - amount: 1000000
   ```

3. **Approve an asset for use with the smart wallet**
   ```
   Approve a token for use with my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   ```

4. **Check if an asset is approved**
   ```
   Check if the token is approved for my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   ```

5. **Get the smart wallet configuration**
   ```
   Get the configuration of my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   ```

### DEX Trading Workflow

1. **Approve a DEX for trading**
   ```
   Approve a DEX for use with my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
   ```

2. **Allow agent to buy/sell assets**
   ```
   Allow my agent to buy/sell assets through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - can_buy_sell: true
   ```

3. **Buy tokens from the DEX**
   ```
   Buy tokens from the DEX through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   - amount: 100
   ```

4. **Sell tokens to the DEX**
   ```
   Sell tokens to the DEX through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token-dex
   - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   - amount: 50
   ```

### DAO Governance Workflow

1. **Propose an action to the DAO**
   ```
   Propose an action to the DAO through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - action_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2
   - action_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-send-message
   - parameters: "Hello, DAO!"
   ```

2. **Vote on an action proposal**
   ```
   Vote on an action proposal through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - action_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-action-proposals-v2
   - proposal_id: 123
   - vote: true
   ```

3. **Create a core proposal**
   ```
   Create a core proposal through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
   - proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
   - dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   ```

4. **Vote on a core proposal**
   ```
   Vote on a core proposal through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
   - proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
   - vote: true
   ```

5. **Conclude a proposal**
   ```
   Conclude a core proposal through my smart wallet:
   - smart_wallet_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG
   - core_proposals_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-core-proposals-v2
   - proposal_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.proposal-add-extension
   - dao_token_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-token
   ```

## Error Handling

All Smart Wallet tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Unauthorized access",
  "code": 9000
}
```

Common error codes:
- 9000: Unauthorized access (caller is not authorized)
- 9001: Unknown asset (asset is not in the approved list)
- 9002: Operation failed (general operation failure)
- 9003: Buy/sell not allowed (agent does not have permission to buy/sell)
- 9004: Smart wallet not found
- 9005: Asset already approved
- 9006: DEX not approved
- 9007: Insufficient balance
