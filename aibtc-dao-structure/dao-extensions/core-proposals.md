---
description: Manages voting on arbitrary Clarity code execution
---

# Core Proposals Extension

The Core Proposals extension (`aibtc-core-proposals-v2`) enables DAO members to vote on proposals that can execute arbitrary Clarity code in the context of the DAO. This provides the highest level of governance control with correspondingly high voting thresholds.

## Contract Overview

- **Title**: aibtc-core-proposals-v2
- **Version**: 2.0.0
- **Implements**: 
  - `extension` trait
  - `core-proposals` trait

## Voting Configuration

| Parameter | Value | Description |
|-----------|-------|-------------|
| Voting Delay | 432 blocks (~3 days) | Time before voting starts after proposal creation |
| Voting Period | 432 blocks (~3 days) | Duration of the voting period |
| Voting Quorum | 25% | Minimum participation required as percentage of liquid supply |
| Voting Threshold | 90% | Minimum percentage of votes that must be in favor |

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `create-proposal` | Emitted when a new proposal is created | Proposal contract, creator, start/end blocks, liquid tokens |
| `vote-on-proposal` | Emitted when a vote is cast on a proposal | Proposal contract, voter, vote amount |
| `conclude-proposal` | Emitted when a proposal is concluded | Proposal contract, vote results, execution status |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `create-proposal` | Create a new core proposal | `proposal`: proposal-trait |
| `vote-on-proposal` | Cast a vote on an existing proposal | `proposal`: proposal-trait, `vote`: bool |
| `conclude-proposal` | Conclude a proposal after voting period | `proposal`: proposal-trait |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `get-voting-power` | Get voting power of an address for a proposal | `who`: principal, `proposal`: proposal-trait |
| `get-proposal` | Get details of a proposal | `proposal`: principal |
| `get-vote-record` | Get vote record for a specific voter | `proposal`: principal, `voter`: principal |
| `get-total-proposals` | Get total number of proposals | None |
| `get-last-proposal-created` | Get block height of last proposal | None |
| `get-voting-configuration` | Get voting configuration details | None |
| `get-liquid-supply` | Calculate liquid supply of DAO token | `blockHeight`: uint |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u3000 | ERR_NOT_DAO_OR_EXTENSION | Caller is not the DAO or an extension |
| u3001 | ERR_FETCHING_TOKEN_DATA | Error fetching token data |
| u3002 | ERR_INSUFFICIENT_BALANCE | Caller has insufficient token balance |
| u3003 | ERR_PROPOSAL_NOT_FOUND | Proposal not found |
| u3004 | ERR_PROPOSAL_ALREADY_EXECUTED | Proposal already executed |
| u3005 | ERR_PROPOSAL_VOTING_ACTIVE | Proposal voting is still active |
| u3006 | ERR_PROPOSAL_EXECUTION_DELAY | Proposal is in execution delay period |
| u3007 | ERR_SAVING_PROPOSAL | Error saving proposal |
| u3008 | ERR_PROPOSAL_ALREADY_CONCLUDED | Proposal already concluded |
| u3009 | ERR_RETRIEVING_START_BLOCK_HASH | Error retrieving start block hash |
| u3010 | ERR_VOTE_TOO_SOON | Vote attempted before voting period started |
| u3011 | ERR_VOTE_TOO_LATE | Vote attempted after voting period ended |
| u3012 | ERR_ALREADY_VOTED | User already voted on this proposal |
| u3013 | ERR_FIRST_VOTING_PERIOD | First voting period has not passed |
| u3014 | ERR_DAO_NOT_ACTIVATED | DAO not activated |

## Liquid Supply Calculation

The liquid supply calculation excludes tokens held by:
- The token DEX contract
- The token pool contract
- The treasury contract

This ensures that only tokens in circulation are counted for voting power.
