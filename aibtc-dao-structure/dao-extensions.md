---
description: Modular components that provide specific functionality to the dao
---

# DAO Extensions

Extensions are what gives the dao form and enable new features.

Extensions can be enabled or disabled in the base dao contract, and should use this check for their operation when appropriate.

Several extensions are included with each dao and more can be added through core proposals.

## Extension List

| Extension | Description | Documentation |
|-----------|-------------|---------------|
| [Action Proposals (aibtc-action-proposals-v2)](./dao-extensions/action-proposals.md) | Manages voting on predefined actions with lower thresholds | [Details](./dao-extensions/action-proposals.md) |
| [Bank Account (aibtc-bank-account)](./dao-extensions/bank-account.md) | Manages periodic STX withdrawals for designated account holder | [Details](./dao-extensions/bank-account.md) |
| [Core Proposals (aibtc-core-proposals-v2)](./dao-extensions/core-proposals.md) | Manages voting on arbitrary Clarity code execution | [Details](./dao-extensions/core-proposals.md) |
| [DAO Charter (aibtc-dao-charter)](./dao-extensions/dao-charter.md) | Manages the DAO charter and records mission and values on-chain | [Details](./dao-extensions/dao-charter.md) |
| [Onchain Messaging (aibtc-onchain-messaging)](./dao-extensions/onchain-messaging.md) | Enables sending verified messages from the DAO | [Details](./dao-extensions/onchain-messaging.md) |
| [Payments/Invoices (aibtc-payments-invoices)](./dao-extensions/payments-invoices.md) | Handles payment processing for DAO services | [Details](./dao-extensions/payments-invoices.md) |
| [Token Owner (aibtc-token-owner)](./dao-extensions/token-owner.md) | Manages the DAO token configuration | [Details](./dao-extensions/token-owner.md) |
| [Treasury (aibtc-treasury)](./dao-extensions/treasury.md) | Manages DAO assets (STX, FTs, NFTs) | [Details](./dao-extensions/treasury.md) |

### Extension Highlights

#### Action Proposals
* 66% approval threshold, 15% quorum
* 1-day voting delay, 2-day voting period
* Limited to whitelisted actions

#### Bank Account
* Configurable withdrawal amount and time period
* Allows STX deposits from anyone
* Withdrawal controls bound by DAO-set parameters

#### Core Proposals
* 90% approval threshold, 25% quorum
* 3-day voting delay, 3-day voting period
* Can execute any valid proposal contract

#### Onchain Messaging
* Supports messages up to 1MB in size
* Messages are stored as blockchain events
* Can be used by anyone, with DAO verification flag

#### Payments/Invoices
* Manages resources with prices and descriptions
* Tracks user payment history
* Supports enabling/disabling resources

#### DAO Charter
* Records the organization's mission and values on-chain
* Maintains versioned history of all charter changes
* Supports optional inscription IDs for blockchain permanence

#### Token Owner
* Controls token URI updates
* Handles ownership transfers
* Executes token management functions

#### Treasury
* Controls asset allowlist
* Handles deposits and withdrawals
* Supports STX stacking delegation

### Additional Components

* **Base Dao:** core contract managing extensions and proposal execution
* **Token**: split 80% to dao treasury / 20% to dex
* **Token DEX:** handles initial token distribution and price discovery
* **Bitflow Pool:** provides liquidity pool after initial DEX phase

### Key Features

* Extensions can be enabled/disabled via proposals
* Each extension implements specific trait(s)
* Extensions can interact with each other through the DAO
* All sensitive operations require proposal approval
