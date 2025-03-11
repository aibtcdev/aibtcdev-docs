---
description: Overview of the agent tools system
---

# Agent Tools

Agent tools are modular components that provide specific functionality to AI agents. They allow agents to interact with blockchain networks, manage wallets, interact with DAOs, and perform various other tasks.

## How Agent Tools Work

Each tool:
- Has a specific purpose and functionality
- Can be enabled or disabled for specific agents
- Has clear input and output specifications
- Provides error handling and feedback

## Tool Architecture

Tools follow a consistent pattern:
1. **Input Schema**: Each tool has a defined input schema using Pydantic models
2. **Execution Logic**: Tools contain the logic to perform their specific function
3. **Error Handling**: Tools provide standardized error responses
4. **Return Values**: Tools return structured data that can be parsed by agents

## Available Tool Categories

| Category | Purpose | Key Features |
|----------|---------|--------------|
| [Wallet Tools](wallet-tools.md) | Manage cryptocurrency wallets | Balance checking, transactions, address management |
| [DAO Tools](dao-tools.md) | Interact with DAOs | Proposal management, voting, extension interaction |
| [Faktory Tools](faktory-tools.md) | Interact with Faktory DEX | Token swaps, liquidity management, price quotes |
| [Database Tools](database-tools.md) | Manage persistent data | Scheduled tasks, DAO information, configuration |

## Tool Security

Tools follow these security principles:
- Tools verify caller permissions where necessary
- Critical operations require explicit confirmation
- Tools use standardized error handling
- Tools emit detailed logs for auditing purposes

For detailed documentation on each tool category, see the individual tool pages.
