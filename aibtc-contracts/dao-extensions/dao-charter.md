---
description: Manages the DAO charter and records the DAO's mission and values on-chain
---

# DAO Charter Extension

The DAO Charter extension (`aibtc-dao-charter`) allows the DAO to define and maintain its mission and values on-chain. This provides a permanent record of the organization's purpose and principles that can guide decision-making and proposals.

## Contract Overview

- **Title**: aibtc-dao-charter
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `charter` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `set-dao-charter` | Emitted when the charter is updated | Charter text, version, creator, timestamp, optional inscription ID |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `set-dao-charter` | Set or update the DAO charter | `charter`: string-ascii 4096, `inscriptionId`: optional buff 33 |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `get-current-dao-charter-version` | Get the current charter version | None |
| `get-current-dao-charter` | Get the current charter text | None |
| `get-dao-charter` | Get a specific version of the charter | `version`: uint |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u8000 | ERR_NOT_DAO_OR_EXTENSION | Caller is not the DAO or an extension |
| u8001 | ERR_SAVING_CHARTER | Error saving charter data |
| u8002 | ERR_CHARTER_TOO_SHORT | Charter text is too short |
| u8003 | ERR_CHARTER_TOO_LONG | Charter text exceeds maximum length |

## Charter Versioning

The contract maintains a history of all charter versions, including:
- Charter text (up to 4096 ASCII characters)
- Creation timestamp (block height)
- Creator information
- Optional inscription ID for blockchain permanence

Each update creates a new version while preserving the complete history of previous versions.

## Usage

The charter serves as a foundational document for the DAO, establishing:
- The organization's mission and purpose
- Core values and principles
- Governance philosophy
- Long-term vision and goals

Changes to the charter require approval through the DAO's governance process, ensuring that fundamental changes to the organization's direction have broad support from token holders.
