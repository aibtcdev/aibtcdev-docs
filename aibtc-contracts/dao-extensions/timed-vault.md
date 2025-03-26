---
description: Manages periodic STX withdrawals for designated account holder
---

# Timed Vault Extension

The Timed Vault extension (`aibtc-timed-vault`) provides a mechanism for periodic STX withdrawals by a designated account holder. This extension is useful for managing operational expenses or recurring payments with controlled withdrawal limits.

## Contract Overview

- **Title**: aibtc-timed-vault
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `timed-vault` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `deposit-stx` | Emitted when STX is deposited | Amount, caller, recipient |
| `withdraw-stx` | Emitted when STX is withdrawn | Amount, caller, recipient |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `set-account-holder` | Set the account holder who can withdraw | `new`: principal |
| `set-withdrawal-period` | Set the minimum time between withdrawals | `period`: uint |
| `set-withdrawal-amount` | Set the amount that can be withdrawn | `amount`: uint |
| `override-last-withdrawal-block` | Override the last withdrawal block | `block`: uint |
| `deposit-stx` | Deposit STX to the account | `amount`: uint |
| `withdraw-stx` | Withdraw STX from the account | None |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `get-deployed-block` | Get the block height when deployed | None |
| `get-account-balance` | Get the current STX balance | None |
| `get-account-holder` | Get the current account holder | None |
| `get-last-withdrawal-block` | Get the block of the last withdrawal | None |
| `get-withdrawal-period` | Get the minimum period between withdrawals | None |
| `get-withdrawal-amount` | Get the amount that can be withdrawn | None |
| `get-account-terms` | Get all account configuration details | None |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u2000 | ERR_INVALID | Invalid parameter value |
| u2001 | ERR_UNAUTHORIZED | Caller is not authorized |
| u2002 | ERR_TOO_SOON | Withdrawal attempted too soon |
| u2003 | ERR_INVALID_AMOUNT | Invalid amount specified |

## Default Configuration

- Default withdrawal period: 144 blocks (~1 day)
- Default withdrawal amount: 10 STX
- Default account holder: Contract itself (must be changed by DAO)

## Security Features

- Only the account holder can withdraw funds
- Withdrawals are limited by amount and frequency
- Only the DAO can change account parameters
- Anyone can deposit STX to the account
