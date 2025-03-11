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
| [Smart Wallet Tools](smartwallet-tools.md) | Manage programmable wallets | Deployment, asset management, configuration |

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

### Action Proposal Walkthrough

Here's a complete walkthrough for creating and managing an action proposal:

1. **Check wallet balance**
   ```
   Check your wallet balance and report the balances of STX and sBTC.
   ```

2. **Get testnet STX (if needed)**
   ```
   Fund my wallet with STX from the testnet faucet.
   ```

3. **Get testnet sBTC (if needed)**
   ```
   Request testnet sBTC from the Faktory faucet.
   ```

4. **Buy DAO tokens to participate**
   ```
   Execute a buy order for FACES on the Faktory DEX with the following details:
   - btc_amount: 0.0002
   - dao_token_dex_contract_address: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-faktory
   ```

5. **Create an action proposal**
   ```
   Propose sending the message "LFG!" from the FACES dao
   - dao_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-proposals-v2
   - action_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-send-message
   ```

6. **Get proposal information**
   ```
   Get the transaction details from 0x3cc19a5aa3ba3af9e14716e3a988de748b9bc034efd4fa13f7d30c00a901ff9f and provide the tx_status, the proposal ID, start and end blocks, and liquid tokens.
   ```

7. **Check proposal details**
   ```
   What can you tell me about proposal 11 in the FACES DAO?
   - dao_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-proposals-v2
   ```

8. **Vote on the proposal**
   ```
   Vote yes on proposal 11 in the FACES dao.
   - dao_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-proposals-v2
   - proposal_id: 11
   - vote: for
   - amount: 1000000
   ```

9. **Conclude the proposal**
   ```
   Conclude proposal 11 in the faces dao
   - dao_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-proposals-v2
   - action_contract: ST3YT0XW92E6T2FE59B2G5N2WNNFSBZ6MZKQS5D18.faces-action-send-message
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
