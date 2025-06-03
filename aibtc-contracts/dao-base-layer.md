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

- Action Proposals: Predefined actions, faster voting, veto, rewards
- DAO Charter: Mission and values / On-chain organizational constitution
- DAO Epoch: Bitcoin block-based epochs, configurable length
- DAO Users: User registration, reputation tracking
- Onchain Messaging: Verified DAO/user messages, permanent records via print events
- Rewards Account: Securely holds and transfers SIP-010 token rewards
- Token Owner: DAO Token URI updates, ownership controls
- Treasury: Fungible token (SIP-010) support, controlled access

## Proposal System

The DAO is governed entirely by token holders through proposals. Currently, this is primarily facilitated through Action Proposals.

**Action Proposals**:

- Used for predefined operations, such as sending on-chain messages.
- Feature lower voting thresholds (e.g., 66% approval, 15% quorum).
- Follow a lifecycle of creation, voting, conclusion, and execution.

These proposals are designed for routine DAO operations within set parameters.

## Tools and Interaction

The DAO provides various tools for interacting with its contracts:

- Read-only functions to check proposal status and extension configuration
- Transaction functions to submit proposals and execute DAO operations
- Helper utilities for common operations

For detailed documentation on each component, see the individual pages for [extensions](dao-extensions/README.md) and [proposals](dao-proposals/README.md).
