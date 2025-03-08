---
description: Manages the DAO token configuration
---

# Token Owner Extension

The Token Owner extension (`aibtc-token-owner`) provides management functions for the DAO token. It allows the DAO to control token metadata and ownership through governance.

## Contract Overview

- **Title**: aibtc-token-owner
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `token-owner` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| None | The contract does not emit specific events | N/A |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `set-token-uri` | Update the token URI metadata | `value`: string-utf8 256 |
| `transfer-ownership` | Transfer token ownership to a new principal | `new-owner`: principal |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| None | The contract does not provide read-only functions | N/A |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u7000 | ERR_UNAUTHORIZED | Caller is not the DAO or an extension |

## Token Management

The extension provides two key management functions:

1. **Token URI Management**: 
   - Updates the token's URI metadata
   - Controls how the token appears in wallets and explorers
   - Can point to decentralized storage for token information

2. **Ownership Transfer**:
   - Allows the DAO to transfer token contract ownership
   - Provides flexibility for contract upgrades or governance changes
   - Executed through DAO proposals for security

## Security Features

- All functions can only be called by the DAO or authorized extensions
- Changes require proposal approval through governance
- The extension uses the contract-call? pattern to execute functions with proper permissions
