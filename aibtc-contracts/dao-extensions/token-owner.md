---
description: Extension that provides management functions for the DAO token
---

# Token Owner Extension

The Token Owner extension (`aibtc-token-owner`) provides management functions for the DAO token, allowing the DAO to control token metadata and ownership through governance. This extension serves as the authorized interface between the DAO and its token contract, ensuring that token configuration changes can only be executed through proper governance channels.

## Key Features

- **Token URI Management**: Updates the token's metadata URI through governance
- **Ownership Control**: Allows the DAO to transfer token contract ownership
- **Permission Gating**: Ensures only the DAO or authorized extensions can modify token settings
- **Contract Interoperability**: Interfaces between the DAO and token contract using proper permissions

## Quick Reference

| Property       | Value                                |
| -------------- | ------------------------------------ |
| Contract Name  | `aibtc-token-owner`                 |
| Version        | 1.0.0                               |
| Implements     | `.aibtc-dao-traits.extension`, `.aibtc-dao-traits.token-owner` |
| Key Parameters | None (stateless extension)          |

## How It Works

```mermaid
flowchart TD
    A["DAO Contract"]
    B["Token Owner Extension"]
    C["Token Contract"]
    D["Updated Token URI"]
    E["New Token Owner"]
    
    subgraph Extension Functions
        BA["set-token-uri"]
        BB["transfer-ownership"]
    end
    
    A -->|"Proposal Execution"| B
    B --> BA
    B --> BB
    BA -->|"Updates metadata"| C
    BB -->|"Changes ownership"| C
    C --> D
    C --> E
```

The Token Owner extension acts as an authorized intermediary between the DAO and its token contract. When the DAO approves a proposal to update token settings, it calls the appropriate function on this extension. The extension verifies the caller is authorized (either the DAO itself or another approved extension), then uses `as-contract` to call the token contract with the proper permissions.

## Public Functions

### `callback`

**Purpose**: Standard extension callback function required by the extension trait

**Parameters**:

- `sender`: principal - The principal that triggered the callback
- `memo`: (buff 34) - Optional memo data

**Returns**: (response bool) - Returns true on success

**Example**:

```clarity
(contract-call? .aibtc-token-owner callback tx-sender 0x)
```

### `set-token-uri`

**Purpose**: Updates the token's URI metadata, which controls how the token appears in wallets and explorers

**Parameters**:

- `value`: (string-utf8 256) - The new URI string for the token metadata

**Returns**: (response bool) - Returns true on success or an error

**Example**:

```clarity
(contract-call? .aibtc-token-owner set-token-uri "https://example.com/token-metadata.json")
```

This function can only be called by the DAO or an authorized extension. It updates the token's metadata URI, which typically points to a JSON file containing token information like name, symbol, description, and image.

### `transfer-ownership`

**Purpose**: Transfers token contract ownership to a new principal

**Parameters**:

- `new-owner`: principal - The principal that will become the new token contract owner

**Returns**: (response bool) - Returns true on success or an error

**Example**:

```clarity
(contract-call? .aibtc-token-owner transfer-ownership 'SP2ZNGJ85ENDY6QRHQ5P2D4FXKGZWCKTB2T0Z55KS)
```

This function allows the DAO to transfer ownership of the token contract to a new principal, which could be useful during contract upgrades or governance changes.

## Private Functions

### `is-dao-or-extension`

**Purpose**: Internal authorization check to ensure only the DAO or authorized extensions can call sensitive functions.

**Parameters**: None

**Returns**: `(response bool err-code)` - Returns `(ok true)` if authorized, or `ERR_NOT_DAO_OR_EXTENSION (err u1800)` if unauthorized.

## Error Handling

| Error Code | Constant                  | Description                                | Resolution                                                                 |
| ---------- | ------------------------- | ------------------------------------------ | -------------------------------------------------------------------------- |
| u1800      | ERR_NOT_DAO_OR_EXTENSION  | Caller is not the DAO or a valid extension. | Ensure the function is called through proper DAO governance (e.g., via a proposal). |

## Security Considerations

- **Authorization Control**: All management functions are protected by the `is-dao-or-extension` check, ensuring only authorized entities can modify token settings
- **Contract-Call Pattern**: Uses the `as-contract` pattern to make calls to the token contract with the extension's authority
- **Governance Protection**: Changes to token settings require going through the DAO's proposal and voting process
- **No Direct State**: The extension maintains no state of its own, reducing attack surface
- **Limited Functionality**: The extension provides only the minimum necessary functions for token management

## Integration Examples

### Updating Token URI Through a Proposal

```clarity
;; This would typically be done through a DAO proposal.
;; Example: A proposal contract (.proposal-to-set-uri) calls .aibtc-token-owner
(contract-call? .aibtc-base-dao execute 
  .proposal-to-set-uri ;; This is a hypothetical proposal contract
  'SP000000000000000000002Q6VF78.proposal-sender ;; Example sender
)
;; Where .proposal-to-set-uri would contain:
;; (contract-call? .aibtc-token-owner set-token-uri "https://arweave.net/newTokenMetadata")
```

### Transferring Token Ownership

```clarity
;; This would typically be done through a DAO proposal.
;; Example: A proposal contract (.proposal-to-transfer-ownership) calls .aibtc-token-owner
(contract-call? .aibtc-base-dao execute
  .proposal-to-transfer-ownership ;; This is a hypothetical proposal contract
  'SP000000000000000000002Q6VF78.proposal-sender ;; Example sender
)
;; Where .proposal-to-transfer-ownership would contain:
;; (contract-call? .aibtc-token-owner transfer-ownership 'SP2ZNGJ85ENDY6QRHQ5P2D4FXKGZWCKTB2T0Z55KS)
```

## Related Contracts

- **`.aibtc-faktory`**: The DAO token contract (SIP-010 FT) managed by this extension.
- **`.aibtc-base-dao`**: The core DAO contract that authorizes this extension's actions.
- **`.aibtc-dao-traits.extension`**: Trait implemented by this extension.
- **`.aibtc-dao-traits.token-owner`**: Trait implemented by this extension.

## Review Checklist

- [x] Follows the appropriate template structure
- [x] Includes all required sections
- [x] Has exactly one H1 title
- [x] YAML frontmatter is at the top with description
- [x] Introduction follows immediately after title
- [x] Heading levels are used correctly (H1 → H2 → H3)
- [x] Code examples are complete and functional with language identifiers
- [x] Tables have clear headers and consistent formatting
- [x] Contract diagram has explanation
- [x] Links to related documentation are correct
- [x] No spelling or grammatical errors
- [x] Technical accuracy has been verified
- [x] Examples use realistic values
- [x] Security considerations are addressed comprehensively
- [x] Error codes and handling are documented
- [x] Content is accessible to the target audience

## Versioning and Updates

- **Last Updated**: June 2025
- **Contract Version**: 1.0.0
- **Documentation Version**: 1.2.0
- **Changes from Previous Version**: Updated to match new documentation template format and reflect current contract trait paths.
