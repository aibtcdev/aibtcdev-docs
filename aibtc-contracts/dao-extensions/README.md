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

| Extension                                     | Purpose             | Key Features                                                   |
| --------------------------------------------- | ------------------- | -------------------------------------------------------------- |
| [Action Proposals](action-proposal-voting.md) | On-chain governance | Predefined actions, faster voting, veto, rewards               |
| [DAO Charter](dao-charter.md)                 | Mission and values  | On-chain organizational constitution                           |
| [DAO Epoch](dao-epoch.md)                     | Time tracking       | Bitcoin block-based epochs, configurable length                |
| [DAO Users](dao-users.md)                     | User management     | User registration, reputation tracking                         |
| [Onchain Messaging](onchain-messaging.md)     | Communication       | Verified DAO/user messages, permanent records via print events |
| [Rewards Account](rewards-account.md)         | Reward disbursement | Securely holds and transfers SIP-010 token rewards             |
| [Token Owner](token-owner.md)                 | Token management    | DAO Token URI updates, ownership controls                      |
| [Treasury](treasury.md)                       | FT Asset management | Fungible token (SIP-010) support, controlled access            |

## Adding New Extensions

The first cohort of AIBTC DAOs will not have the ability to add new extensions or modify the operation of the DAO. This scope is intentional to refine the voting and reward mechanisms.

Future iterations of AIBTC DAOs can implement an extension that allows for this and other features.

## Extension Security

Extensions follow these security principles:

- Only the DAO can enable/disable extensions
- Extensions verify caller permissions
- Critical operations require DAO approval
- Extensions use standardized error handling
- Extensions emit events for all important actions

For detailed documentation on each extension, see the individual extension pages.
