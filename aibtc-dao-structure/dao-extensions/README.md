---
description: Overview of the DAO extension system
---

# DAO Extensions

Extensions are modular components that provide specific functionality to the DAO. They allow the DAO to be customized and expanded without modifying the core contract.

## How Extensions Work

Each extension:
- Implements the `extension` trait
- Can be enabled or disabled by the DAO
- Has specific permissions and capabilities
- Interacts with the DAO through a standardized interface

## Extension Architecture

Extensions follow a consistent pattern:
1. **Trait Implementation**: Each extension implements both the base `extension` trait and its own specialized trait
2. **Callback Function**: All extensions have a standard callback function for DAO communication
3. **Permission Checks**: Extensions verify that calls come from authorized sources
4. **Event Logging**: Extensions emit events for important actions
5. **Error Handling**: Extensions use standardized error codes

## Available Extensions

| Extension | Purpose | Key Features |
|-----------|---------|--------------|
| [Action Proposals](./action-proposals.md) | Lower-threshold governance | Predefined actions, faster voting |
| [Bank Account](./bank-account.md) | Operational fund management | Periodic withdrawals, controlled spending |
| [Core Proposals](./core-proposals.md) | High-threshold governance | Arbitrary code execution, high security |
| [DAO Charter](./dao-charter.md) | Mission and values | On-chain organizational constitution |
| [Onchain Messaging](./onchain-messaging.md) | Communication | Verified DAO messages, permanent records |
| [Payments/Invoices](./payments-invoices.md) | Revenue generation | Service payments, resource management |
| [Token Owner](./token-owner.md) | Token management | URI updates, ownership controls |
| [Treasury](./treasury.md) | Asset management | Multi-asset support, controlled access |

## Adding New Extensions

New extensions can be added to the DAO through core proposals. To create a new extension:

1. Implement the `extension` trait
2. Implement any specialized traits needed
3. Follow the standard extension pattern
4. Submit as a core proposal for DAO approval

## Extension Security

Extensions follow these security principles:
- Only the DAO can enable/disable extensions
- Extensions verify caller permissions
- Critical operations require DAO approval
- Extensions use standardized error handling
- Extensions emit events for all important actions

For detailed documentation on each extension, see the individual extension pages.
