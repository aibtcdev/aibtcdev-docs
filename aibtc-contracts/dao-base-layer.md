---
description: The foundation of AIBTC DAOs built on a modular architecture.
---

# DAO Base Layer

## Architecture Overview

The AIBTC DAO is built on a modular architecture that separates core functionality from extensions:

- **Base DAO Contract**: Handles proposal execution and extension management
- **Extensions**: Provide specialized functionality (voting, treasury, messaging, etc.)
- **Proposals**: Smart contracts that can execute arbitrary code when approved

## Core Components

### Base DAO Contract

The base DAO contract (`aibtc-base-dao`) implements the core functionality:

- **Proposal Execution**: Executes approved proposals as smart contracts
- **Extension Management**: Enables/disables extensions that provide additional functionality
- **Authorization Control**: Ensures only authorized entities can perform sensitive operations
- **Event Logging**: Records all significant actions for transparency

### Key Functions

- `construct`: Initializes the DAO with its first proposal
- `execute`: Runs the code in an approved proposal
- `set-extension`: Enables or disables a single extension
- `set-extensions`: Configures multiple extensions at once
- `request-extension-callback`: Allows extensions to communicate with each other

## Extension System

Extensions are modular components that provide specific functionality to the DAO. Each extension:

- Implements the `extension` trait
- Can be enabled or disabled by the DAO
- Has specific permissions and capabilities
- Interacts with the DAO through a standardized interface

Available extensions include:
- Action Proposals: Lower-threshold governance for predefined actions
- Core Proposals: High-threshold governance for arbitrary code execution
- Treasury: Asset management with multi-asset support
- Timed Vault: Operational fund management with periodic withdrawals
- Onchain Messaging: Verified DAO communication
- Payments/Invoices: Revenue generation and service payments
- Token Owner: Token management and URI updates
- DAO Charter: On-chain organizational constitution

## Proposal System

The DAO is governed entirely by token holders through proposals:

1. **Action Proposals**: Predefined operations with lower voting thresholds (66% approval, 15% quorum)
2. **Core Proposals**: Arbitrary code execution with higher thresholds (90% approval, 25% quorum)

All proposals follow a lifecycle of creation, voting, conclusion, and execution.

## Tools and Interaction

The DAO provides various tools for interacting with its contracts:

- Read-only functions to check proposal status and extension configuration
- Transaction functions to submit proposals and execute DAO operations
- Helper utilities for common operations

For detailed documentation on each component, see the individual pages for [extensions](dao-extensions/README.md) and [proposals](dao-proposals/README.md).
