---
description: Tools for interacting with aibtc-agent-account contracts.
---

# Agent Account Tools

Agent Account tools provide functionality for interacting with `aibtc-agent-account` contracts. These contracts act as a secure interface between an owner (user) and an agent, enabling controlled asset management and DAO participation.

## Tool Overview

| Tool Name                              | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ |
| `agentaccount_deposit_stx`             | Deposit STX to an agent account.                             |
| `agentaccount_deposit_ft`              | Deposit fungible tokens to an agent account.                 |
| `agentaccount_approve_contract`        | Approve a contract for interaction (owner or permitted agent). |
| `agentaccount_revoke_contract`         | Revoke a contract's approval (owner or permitted agent).     |
| `agentaccount_create_action_proposal`  | Create a DAO action proposal (owner or permitted agent).     |
| `agentaccount_vote_on_action_proposal` | Vote on a DAO action proposal (owner or permitted agent).    |
| `agentaccount_veto_action_proposal`    | Veto a DAO action proposal (owner or permitted agent).       |
| `agentaccount_conclude_action_proposal`| Conclude a DAO action proposal (owner or permitted agent).   |
| `agentaccount_faktory_buy_asset`       | Buy an asset from a Faktory DEX (owner or permitted agent).  |
| `agentaccount_faktory_sell_asset`      | Sell an asset to a Faktory DEX (owner or permitted agent).   |
| `agentaccount_get_configuration`       | Get the configuration of an agent account.                   |
| `agentaccount_is_approved_contract`    | Check if a contract is approved.                             |

## Tool Details

### `agentaccount_deposit_stx`

Deposits STX into an agent account. Can be called by the owner or the agent.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `amount`: Amount of STX to deposit in microstacks.

**Output**:
```json
{
  "success": true,
  "txid": "0x1234...",
  "amount": 1000000,
  "recipient": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-..."
}
```

### `agentaccount_deposit_ft`

Deposits fungible tokens into an agent account. Can be called by the owner or the agent. The token contract must be approved first.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `ft_contract`: Contract principal of the fungible token.
- `amount`: Amount of tokens to deposit (in the token's smallest unit).

**Output**:
```json
{
  "success": true,
  "txid": "0x2345...",
  "amount": 5000,
  "token_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.some-token",
  "recipient": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-..."
}
```

### `agentaccount_approve_contract`

Approves a contract for interaction. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `contract_to_approve`: The principal of the contract to approve.

**Output**:
```json
{
  "success": true,
  "txid": "0x3456...",
  "approved_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory-dex"
}
```

### `agentaccount_revoke_contract`

Revokes a contract's approval. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `contract_to_revoke`: The principal of the contract to revoke.

**Output**:
```json
{
  "success": true,
  "txid": "0x4567...",
  "revoked_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory-dex"
}
```

### `agentaccount_create_action_proposal`

Creates an action proposal via an approved voting contract. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `voting_contract`: The principal of the action proposal voting contract.
- `action_contract`: The principal of the action to be proposed.
- `parameters`: `(buff 2048)` - ABI-encoded parameters for the action.
- `memo`: `(optional (string-ascii 1024))` - An optional memo.

**Output**:
```json
{
  "success": true,
  "txid": "0x5678...",
  "proposal_contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.action-proposal-voting"
}
```

### `agentaccount_vote_on_action_proposal`

Votes on an action proposal. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `voting_contract`: The principal of the action proposal voting contract.
- `proposal_id`: The ID of the proposal to vote on.
- `vote`: `bool` - `true` for yes, `false` for no.

**Output**:
```json
{
  "success": true,
  "txid": "0x6789...",
  "proposal_id": 1,
  "vote": true
}
```

### `agentaccount_veto_action_proposal`

Vetoes an action proposal. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `voting_contract`: The principal of the action proposal voting contract.
- `proposal_id`: The ID of the proposal to veto.

**Output**:
```json
{
  "success": true,
  "txid": "0xabcd...",
  "proposal_id": 1,
  "vetoed": true
}
```

### `agentaccount_conclude_action_proposal`

Concludes an action proposal. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `voting_contract`: The principal of the action proposal voting contract.
- `proposal_id`: The ID of the proposal to conclude.
- `action_contract`: The principal of the action contract associated with the proposal.

**Output**:
```json
{
  "success": true,
  "txid": "0xbcde...",
  "proposal_id": 1,
  "concluded": true
}
```

### `agentaccount_faktory_buy_asset`

Buys an asset from an approved Faktory DEX. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `faktory_dex_contract`: The principal of the Faktory DEX.
- `asset_contract`: The principal of the asset to buy.
- `amount`: The amount of the asset to buy.

**Output**:
```json
{
  "success": true,
  "txid": "0x789a...",
  "asset_bought": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.some-faktory-token",
  "amount": 10000
}
```

### `agentaccount_faktory_sell_asset`

Sells an asset to an approved Faktory DEX. Can be called by the owner, or the agent if permitted.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `faktory_dex_contract`: The principal of the Faktory DEX.
- `asset_contract`: The principal of the asset to sell.
- `amount`: The amount of the asset to sell.

**Output**:
```json
{
  "success": true,
  "txid": "0xcdef...",
  "asset_sold": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.some-faktory-token",
  "amount": 5000
}
```

### `agentaccount_get_configuration`

Gets the configuration of an agent account. This is a read-only tool.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.

**Output**:
```json
{
  "account": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...",
  "owner": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "agent": "ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG",
  "sbtc": "STV9K21TBFAK4KNRJXF5DFP8N7W46G4V9RJ5XDY2.sbtc-token"
}
```

### `agentaccount_is_approved_contract`

Checks if a specific contract is approved in the agent account. This is a read-only tool.

**Input Parameters**:
- `agent_account_contract`: Contract principal of the agent account.
- `contract_to_check`: The principal of the contract to check.

**Output**:
```json
{
  "approved": true,
  "contract": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory-dex"
}
```

## Workflow Examples

### DAO Governance Workflow

1.  **Approve the DAO's voting contract**
    *Note: This can be done by the owner, or the agent if `agentCanApproveRevokeContracts` is `true`.*
    ```
    Approve a contract for my agent account:
    - agent_account_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...
    - contract_to_approve: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.action-proposal-voting
    ```

2.  **Create a new proposal**
    *Note: This can be done by the owner, or the agent if `agentCanUseProposals` is `true`.*
    ```
    Create an action proposal using my agent account:
    - agent_account_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...
    - voting_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.action-proposal-voting
    - action_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.some-action
    - parameters: 0x...
    ```

3.  **Vote on the proposal**
    ```
    Vote on an action proposal using my agent account:
    - agent_account_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...
    - voting_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.action-proposal-voting
    - proposal_id: 1
    - vote: true
    ```

### DEX Trading Workflow

1.  **Approve the DEX contract**
    *Note: This can be done by the owner, or the agent if `agentCanApproveRevokeContracts` is `true`.*
    ```
    Approve a DEX for my agent account:
    - agent_account_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...
    - contract_to_approve: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory-dex
    ```

2.  **Buy an asset**
    *Note: This can only be done if the owner has enabled trading for the agent by calling `set-agent-can-buy-sell-assets(true)` directly on the contract.*
    ```
    Buy an asset using my agent account:
    - agent_account_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-agent-account-...
    - faktory_dex_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.aibtc-faktory-dex
    - asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.some-faktory-token
    - amount: 10000
    ```

## Error Handling

The Agent Account tools return standardized error responses based on the contract's error codes:

```json
{
  "success": false,
  "error": "Caller is not the owner.",
  "code": "u1100"
}
```

| Error Code | Constant                    | Description                               |
| ---------- | --------------------------- | ----------------------------------------- |
| `u1100`    | `ERR_CALLER_NOT_OWNER`      | Caller is not the owner.                  |
| `u1101`    | `ERR_CONTRACT_NOT_APPROVED` | The target contract is not approved.      |
| `u1103`    | `ERR_OPERATION_NOT_ALLOWED` | The caller cannot perform this action.    |
