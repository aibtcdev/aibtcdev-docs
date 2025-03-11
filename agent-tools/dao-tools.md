---
description: Tools for interacting with DAOs
---

# DAO Tools

DAO tools provide functionality for interacting with DAOs, managing proposals, voting, and working with DAO extensions.

## Tool Overview

| Tool Name | Description | Key Features |
|-----------|-------------|--------------|
| `dao_actionproposals_get_proposal` | Get details of an action proposal | Proposal status, voting info |
| `dao_actionproposals_vote_on_proposal` | Vote on an action proposal | For/against voting, vote tracking |
| `dao_bank_deposit_stx` | Deposit STX to a DAO's bank account | Transaction creation, receipt |
| `dao_bank_withdraw_stx` | Withdraw STX from a DAO's bank account | Authorization check, receipt |
| `dao_charter_get_current` | Get the current DAO charter | Full charter text, version info |
| `dao_payments_get_invoice` | Get details of a payment invoice | Invoice status, payment details |
| `dao_treasury_is_allowed_asset` | Check if an asset is allowed in treasury | Asset validation |

## Tool Details

### dao_actionproposals_get_proposal

Retrieves details about a specific action proposal.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO
- `proposal_id`: ID of the proposal to retrieve

**Output**:
```json
{
  "id": 1,
  "title": "Add new resource",
  "description": "Add a new resource for the DAO",
  "proposer": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "status": "active",
  "votes_for": 1000000,
  "votes_against": 500000,
  "start_block_height": 12345,
  "end_block_height": 12545,
  "action_data": {
    "type": "add-resource",
    "name": "developer",
    "rate": 100
  }
}
```

**Example Prompt**:
```
Get details about a specific action proposal:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
- proposal_id: 1
```

### dao_actionproposals_vote_on_proposal

Votes on an action proposal.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO
- `proposal_id`: ID of the proposal to vote on
- `vote`: "for" or "against"
- `amount`: Amount of voting power to use

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "vote": "for",
  "amount": 1000000
}
```

**Example Prompt**:
```
Vote on an action proposal:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
- proposal_id: 1
- vote: for
- amount: 1000000
```

### dao_bank_deposit_stx

Deposits STX to a DAO's bank account.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO
- `amount`: Amount of STX to deposit

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 1000000,
  "new_balance": 5000000
}
```

**Example Prompt**:
```
Deposit STX to a DAO's bank account:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
- amount: 1000000
```

### dao_bank_withdraw_stx

Withdraws STX from a DAO's bank account (requires authorization).

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO

**Output**:
```json
{
  "success": true,
  "txid": "0x8912c9f4a79114eb4bdb153fc35fa3d3cddd3c681a855a8f2f27ab5799f552c0",
  "amount": 1000000,
  "new_balance": 4000000
}
```

**Example Prompt**:
```
Withdraw STX from a DAO's bank account:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
```

### dao_charter_get_current

Retrieves the current charter for a DAO.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO

**Output**:
```json
{
  "version": 1,
  "title": "DAO Charter",
  "content": "This DAO is dedicated to...",
  "created_at": 12345,
  "author": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM"
}
```

**Example Prompt**:
```
Get the current charter for a DAO:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
```

### dao_payments_get_invoice

Retrieves details about a specific invoice.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO
- `invoice_id`: ID of the invoice to retrieve

**Output**:
```json
{
  "id": 1,
  "resource_id": 2,
  "resource_name": "developer",
  "amount": 1000,
  "status": "pending",
  "created_by": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM",
  "created_at": 12345,
  "description": "Development work for March"
}
```

**Example Prompt**:
```
Get details about a specific invoice:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
- invoice_id: 1
```

### dao_treasury_is_allowed_asset

Checks if an asset is allowed in the DAO's treasury.

**Input Parameters**:
- `dao_contract`: Contract principal of the DAO
- `asset_contract`: Contract principal of the asset

**Output**:
```json
{
  "allowed": true,
  "asset": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token",
  "since_block": 12345
}
```

**Example Prompt**:
```
Check if an asset is allowed in the DAO's treasury:
- dao_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao
- asset_contract: ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token
```

## Error Handling

All DAO tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Unauthorized access",
  "code": 5001
}
```

Common error codes:
- 5001: Unauthorized access
- 5002: Proposal not found
- 5003: Invalid vote
- 5004: Insufficient voting power
- 5005: Proposal expired
