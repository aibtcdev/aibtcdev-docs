---
description: Manages voting on predefined actions with lower thresholds
---

# Action Proposals Extension

The Action Proposals extension (`aibtc-action-proposals-v2`) enables DAO members to vote on predefined actions with lower thresholds than core proposals. This allows for more routine operations to be executed without the high barriers required for fundamental changes to the DAO.

## Contract Overview

- **Title**: aibtc-action-proposals-v2
- **Version**: 2.0.0
- **Implements**: 
  - `extension` trait
  - `action-proposals` trait

## Voting Configuration

| Parameter | Value | Description |
|-----------|-------|-------------|
| Voting Delay | 144 blocks (~1 day) | Time before voting starts after proposal creation |
| Voting Period | 288 blocks (~2 days) | Duration of the voting period |
| Voting Quorum | 15% | Minimum participation required as percentage of liquid supply |
| Voting Threshold | 66% | Minimum percentage of votes that must be in favor |

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `propose-action` | Emitted when a new action proposal is created | Proposal ID, action contract, parameters, creator, start/end blocks |
| `vote-on-proposal` | Emitted when a vote is cast on a proposal | Proposal ID, voter, vote amount |
| `conclude-proposal` | Emitted when a proposal is concluded | Proposal ID, vote results, execution status |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `propose-action` | Create a new action proposal | `action`: action-trait, `parameters`: buff 2048 |
| `vote-on-proposal` | Cast a vote on an existing proposal | `proposalId`: uint, `vote`: bool |
| `conclude-proposal` | Conclude a proposal after voting period | `proposalId`: uint, `action`: action-trait |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `get-voting-power` | Get voting power of an address for a proposal | `who`: principal, `proposalId`: uint |
| `get-proposal` | Get details of a proposal | `proposalId`: uint |
| `get-vote-record` | Get vote record for a specific voter | `proposalId`: uint, `voter`: principal |
| `get-total-proposals` | Get total number of proposals | None |
| `get-last-proposal-created` | Get block height of last proposal | None |
| `get-voting-configuration` | Get voting configuration details | None |
| `get-liquid-supply` | Calculate liquid supply of DAO token | `blockHeight`: uint |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u1000 | ERR_NOT_DAO_OR_EXTENSION | Caller is not the DAO or an extension |
| u1001 | ERR_INSUFFICIENT_BALANCE | Caller has insufficient token balance |
| u1002 | ERR_FETCHING_TOKEN_DATA | Error fetching token data |
| u1003 | ERR_PROPOSAL_NOT_FOUND | Proposal not found |
| u1004 | ERR_PROPOSAL_VOTING_ACTIVE | Proposal voting is still active |
| u1005 | ERR_PROPOSAL_EXECUTION_DELAY | Proposal is in execution delay period |
| u1006 | ERR_ALREADY_PROPOSAL_AT_BLOCK | Already a proposal at this block |
| u1007 | ERR_SAVING_PROPOSAL | Error saving proposal |
| u1008 | ERR_PROPOSAL_ALREADY_CONCLUDED | Proposal already concluded |
| u1009 | ERR_RETRIEVING_START_BLOCK_HASH | Error retrieving start block hash |
| u1010 | ERR_VOTE_TOO_SOON | Vote attempted before voting period started |
| u1011 | ERR_VOTE_TOO_LATE | Vote attempted after voting period ended |
| u1012 | ERR_ALREADY_VOTED | User already voted on this proposal |
| u1013 | ERR_INVALID_ACTION | Invalid action contract |
| u1014 | ERR_DAO_NOT_ACTIVATED | DAO not activated |
