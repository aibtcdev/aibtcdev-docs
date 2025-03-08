---
description: Manages DAO assets (STX, FTs, NFTs)
---

# Treasury Extension

The Treasury extension (`aibtc-treasury`) manages all assets owned by the DAO, including STX, SIP-010 fungible tokens, and SIP-009 non-fungible tokens. It provides controlled access to these assets through DAO governance.

## Contract Overview

- **Title**: aibtc-treasury
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `treasury` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `allow-asset` | Emitted when an asset is allowed/disallowed | Token principal, enabled status |
| `deposit-stx` | Emitted when STX is deposited | Amount, sender, recipient |
| `deposit-ft` | Emitted when a fungible token is deposited | Amount, asset contract, sender, recipient |
| `deposit-nft` | Emitted when a non-fungible token is deposited | Asset contract, token ID, sender, recipient |
| `withdraw-stx` | Emitted when STX is withdrawn | Amount, recipient, sender |
| `withdraw-ft` | Emitted when a fungible token is withdrawn | Asset contract, recipient, sender |
| `withdraw-nft` | Emitted when a non-fungible token is withdrawn | Asset contract, token ID, recipient, sender |
| `delegate-stx` | Emitted when STX is delegated for stacking | Amount, delegate address, sender |
| `revoke-delegate-stx` | Emitted when STX delegation is revoked | Sender |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `allow-asset` | Add/update an asset in the allowed list | `token`: principal, `enabled`: bool |
| `allow-assets` | Add/update multiple assets in the allowed list | `allowList`: list of {token, enabled} |
| `deposit-stx` | Deposit STX to the treasury | `amount`: uint |
| `deposit-ft` | Deposit fungible tokens to the treasury | `ft`: ft-trait, `amount`: uint |
| `deposit-nft` | Deposit non-fungible tokens to the treasury | `nft`: nft-trait, `id`: uint |
| `withdraw-stx` | Withdraw STX from the treasury | `amount`: uint, `recipient`: principal |
| `withdraw-ft` | Withdraw fungible tokens from the treasury | `ft`: ft-trait, `amount`: uint, `recipient`: principal |
| `withdraw-nft` | Withdraw non-fungible tokens from the treasury | `nft`: nft-trait, `id`: uint, `recipient`: principal |
| `delegate-stx` | Delegate STX for stacking | `maxAmount`: uint, `to`: principal |
| `revoke-delegate-stx` | Revoke STX delegation | None |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `is-allowed-asset` | Check if an asset is allowed | `assetContract`: principal |
| `get-allowed-asset` | Get allowed status of an asset | `assetContract`: principal |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u6000 | ERR_UNAUTHORIZED | Caller is not the DAO or an extension |
| u6001 | ERR_UNKNOWN_ASSSET | Asset is not in the allowed list |

## Security Features

- All withdrawal functions can only be called by the DAO or authorized extensions
- Assets must be explicitly allowed before they can be deposited or withdrawn
- STX stacking delegation is controlled through DAO governance
