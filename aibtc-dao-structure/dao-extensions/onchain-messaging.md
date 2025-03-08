---
description: Enables sending verified messages from the DAO
---

# Onchain Messaging Extension

The Onchain Messaging extension (`aibtc-onchain-messaging`) allows for sending verified messages that are stored as blockchain events. This provides a way for the DAO to communicate officially and for users to send messages that can be verified as coming from specific addresses.

## Contract Overview

- **Title**: aibtc-onchain-messaging
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `messaging` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| Message content | The actual message content | Raw message string |
| `send` | Metadata about the message | Caller, block height, isFromDao flag, sender |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `send` | Send a message on-chain | `msg`: string-ascii 1048576, `isFromDao`: bool |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u4000 | INPUT_ERROR | Invalid input (empty message) |
| u4001 | ERR_UNAUTHORIZED | Caller is not the DAO or an extension |

## Usage Examples

### Sending a Personal Message
```clarity
(contract-call? .aibtc-onchain-messaging send "Hello, Stacks blockchain!" false)
```

### Sending an Official DAO Message (requires DAO approval)
```clarity
(contract-call? .aibtc-onchain-messaging send "Official announcement from the DAO" true)
```

## Message Size Limits

The extension supports messages up to 1MB in size (1,048,576 ASCII characters), making it suitable for a wide range of communication needs, from simple announcements to more detailed documentation or proposals.
