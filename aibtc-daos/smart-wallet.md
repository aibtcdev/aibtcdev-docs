---
description: User-Agent Smart Wallet for managing assets and DAO interactions
---

# Smart Wallet

The Smart Wallet contract (`aibtc-user-agent-smart-wallet`) provides a secure interface between a user and an agent for managing assets and interacting with DAOs. It enables deposits, withdrawals, and participation in DAO governance through a trusted agent relationship.

## Contract Overview

- **Title**: aibtc-user-agent-smart-wallet
- **Version**: 1.0.0
- **Implements**: `aibtc-smart-wallet` trait

## Print Events

| Event                      | Description                                | Data                                                   |
| -------------------------- | ------------------------------------------ | ------------------------------------------------------ |
| `deposit-stx`              | Emitted when STX is deposited              | Amount, sender, caller, recipient                      |
| `deposit-ft`               | Emitted when a fungible token is deposited | Amount, asset contract, sender, caller, recipient      |
| `withdraw-stx`             | Emitted when STX is withdrawn              | Amount, sender, caller, recipient                      |
| `withdraw-ft`              | Emitted when a fungible token is withdrawn | Amount, asset contract, sender, caller, recipient      |
| `approve-asset`            | Emitted when an asset is approved          | Asset, approved status, sender, caller                 |
| `revoke-asset`             | Emitted when an asset approval is revoked  | Asset, approved status, sender, caller                 |
| `proxy-propose-action`     | Emitted when proposing an action via proxy | Proposal contract, action, parameters, sender, caller  |
| `proxy-create-proposal`    | Emitted when creating a proposal via proxy | Proposal contract, proposal, sender, caller            |
| `vote-on-action-proposal`  | Emitted when voting on an action proposal  | Proposal contract, proposal ID, vote, sender, caller   |
| `vote-on-core-proposal`    | Emitted when voting on a core proposal     | Proposal contract, proposal, vote, sender, caller      |
| `conclude-action-proposal` | Emitted when concluding an action proposal | Proposal contract, proposal ID, action, sender, caller |
| `conclude-core-proposal`   | Emitted when concluding a core proposal    | Proposal contract, proposal, sender, caller            |
| `smart-wallet-created`     | Emitted when the smart wallet is created   | Configuration details                                  |

## Public Functions

### Asset Management Functions

| Function        | Description                                    | Parameters                     |
| --------------- | ---------------------------------------------- | ------------------------------ |
| `deposit-stx`   | Deposit STX to the smart wallet                | `amount`: uint                 |
| `deposit-ft`    | Deposit fungible tokens to the smart wallet    | `ft`: ft-trait, `amount`: uint |
| `withdraw-stx`  | Withdraw STX from the smart wallet             | `amount`: uint                 |
| `withdraw-ft`   | Withdraw fungible tokens from the smart wallet | `ft`: ft-trait, `amount`: uint |
| `approve-asset` | Add an asset to the approved list              | `asset`: principal             |
| `revoke-asset`  | Remove an asset from the approved list         | `asset`: principal             |

### DAO Interaction Functions

| Function                   | Description                          | Parameters                                                                                  |
| -------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------- |
| `proxy-propose-action`     | Propose an action to a DAO via proxy | `action-proposals`: action-proposals-trait, `action`: action-trait, `parameters`: buff 2048 |
| `proxy-create-proposal`    | Create a proposal in a DAO via proxy | `core-proposals`: core-proposals-trait, `proposal`: proposal-trait                          |
| `vote-on-action-proposal`  | Vote on an action proposal           | `action-proposals`: action-proposals-trait, `proposalId`: uint, `vote`: bool                |
| `vote-on-core-proposal`    | Vote on a core proposal              | `core-proposals`: core-proposals-trait, `proposal`: proposal-trait, `vote`: bool            |
| `conclude-action-proposal` | Conclude an action proposal          | `action-proposals`: action-proposals-trait, `proposalId`: uint, `action`: action-trait      |
| `conclude-core-proposal`   | Conclude a core proposal             | `core-proposals`: core-proposals-trait, `proposal`: proposal-trait                          |

## Read-Only Functions

| Function            | Description                             | Parameters         |
| ------------------- | --------------------------------------- | ------------------ |
| `is-approved-asset` | Check if an asset is approved           | `asset`: principal |
| `get-balance-stx`   | Get the STX balance of the smart wallet | None               |
| `get-configuration` | Get the smart wallet configuration      | None               |

## Error Codes

| Code  | Constant             | Description                       |
| ----- | -------------------- | --------------------------------- |
| u1000 | ERR_UNAUTHORIZED     | Caller is not authorized          |
| u1001 | ERR_UNKNOWN_ASSET    | Asset is not in the approved list |
| u1002 | ERR_OPERATION_FAILED | Operation failed                  |

## Security Features

- Only the user can withdraw assets
- Only the user and agent can interact with DAOs
- Assets must be explicitly approved before they can be deposited or withdrawn
- Pre-approved tokens are configured at deployment
- All actions are logged with detailed print events

## Usage Scenarios

### Asset Management

The smart wallet allows users to securely store and manage their assets (STX and fungible tokens) with the following benefits:

- Secure storage with controlled access
- Ability to approve/revoke specific tokens
- Transparent transaction logging

### DAO Participation

The smart wallet enables participation in DAO governance through:

- Proposal creation via proxy
- Voting on proposals
- Concluding proposals

This allows the user to delegate certain DAO interactions to their agent while maintaining control over the assets.

## Deployment Configuration

When deployed, the smart wallet is configured with:

- User principal (wallet owner)
- Agent principal (proposal voter)
- Pre-approved tokens (sBTC and DAO token)

## Contract Naming Convention

Smart wallet contracts follow a specific naming convention:

```
aibtc-smart-wallet-FIRST5-LAST5
```

Where:

- `FIRST5` represents the first 5 characters of the user's Stacks address
- `LAST5` represents the last 5 characters of the user's Stacks address

For example, if an agent were to deploy a smart wallet for `ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM` it would be named:

```
aibtc-smart-wallet-ST1PQ-PGZGM
```

This naming convention ensures that:

1. Each user can have only one smart wallet deployed by a specific agent
2. Smart wallets are easily identifiable by their owner's address
3. One agent can have multiple smart wallet relationships
