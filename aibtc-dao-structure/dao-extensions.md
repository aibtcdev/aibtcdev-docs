---
description: Modular components that provide specific functionality to the dao
---

# DAO Extensions

### Action Proposals (aibtc-action-proposals-v2)

* Manages voting on predefined actions with lower thresholds
* 66% approval threshold, 15% quorum
* 1-day voting delay, 2-day voting period
* Limited to whitelisted actions

### Bank Account (aibtc-bank-account)

* Manages periodic STX withdrawals for designated account holder
* Configurable withdrawal amount and time period
* Allows STX deposits from anyone
* Withdrawal controls bound by DAO-set parameters

### Core Proposals (aibtc-core-proposals-v2)

* Manages voting on arbitrary Clarity code execution
* 90% approval threshold, 25% quorum
* 3-day voting delay, 3-day voting period
* Can execute any valid proposal contract

### Onchain Messaging (aibtc-onchain-messaging)

* Enables sending verified messages from the DAO
* Supports messages up to 1MB in size
* Messages are stored as blockchain events
* Can be used by anyone, with DAO verification flag

### Payments/Invoices (aibtc-payments-invoices)

* Handles payment processing for DAO services
* Manages resources with prices and descriptions
* Tracks user payment history
* Supports enabling/disabling resources

### Token Owner (aibtc-token-owner)

* Manages the DAO token configuration
* Controls token URI updates
* Handles ownership transfers
* Executes token management functions

### Treasury (aibtc-treasury)

* Manages DAO assets (STX, FTs, NFTs)
* Controls asset allowlist
* Handles deposits and withdrawals
* Supports STX stacking delegation

### Additional Components

* **Base Dao:** core contract manging extensions and proposal execution
* **Token**: split 80% to dao treasury / 20% to dex
* **Token DEX:** handles initial token distribution and price discovery
* **Bitflow Pool:** provides liquidity pool after initial DEX phase

### Key Features

* Extensions can be enabled/disabled via proposals
* Each extension implements specific trait(s)
* Extensions can interact with each other through the DAO
* All sensitive operations require proposal approval
