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

## Effective Prompting Patterns

When using agent tools, following consistent prompting patterns helps ensure successful execution. Each prompt should:

1. **Start with a clear action description** that matches the tool's purpose
2. **Include all required parameters** with appropriate values
3. **Use parameter names that match** the tool's expected inputs

### Example Prompting Pattern

```
[Action description that matches tool purpose]
- [parameter1 name]: [parameter1 value]
- [parameter2 name]: [parameter2 value]
```

### Useful Debugging Techniques

When working with tools, these prompting patterns can help with debugging:

- **Get transaction details**

  ```
  Get the details for the TXID 0x3cc19a5aa3ba3af9e14716e3a988de748b9bc034efd4fa13f7d30c00a901ff9f and from those details, tell me the proposal ID and voting period.
  ```

- **Request detailed error information**

  ```
  If you run into an error post the detailed inputs and outputs from the tool so we can debug.
  ```

- **Get transaction history for an address**

  ```
  Tell me more about the last 5 transactions sent by ST43FFM04WT907DE9EXHQPBG3BW7R6R7R6RXZV6C
  ```

- **Get contract transaction history**
  ```
  Tell me more about last 5 transactions in the contract ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-proposals-v2
  ```

## Tool Security

Tools follow these security principles:

- Tools verify caller permissions where necessary
- Critical operations require explicit confirmation
- Tools use standardized error handling
- Tools emit detailed logs for auditing purposes

For detailed documentation on each tool category, see the individual tool pages.

## Related Repositories

The agent tools system is built on two key repositories:

### agent-tools-ts

[agent-tools-ts](https://github.com/aibtcdev/agent-tools-ts) contains the TypeScript implementation of the agent tools, powered by Bun and Stacks.js. This repository provides:

- Low-level blockchain interactions
- Wallet management utilities
- Smart contract interactions
- TypeScript interfaces and implementations
- Command-line tools for testing and development

### aibtcdev-backend

[aibtcdev-backend](https://github.com/aibtcdev/aibtcdev-backend) is the Python backend service that exposes these tools to LLM agents. This repository includes:

- Python wrappers for the TypeScript tools
- FastAPI endpoints for agent interactions
- LangGraph integration for agent workflows
- Background task scheduling
- Database abstractions and models
- Webhook handling for blockchain events
