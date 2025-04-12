---
description: Example of how to use the smart contract documentation template
---

# Smart Wallet Documentation Example

This is an example of how to apply the smart contract documentation template to the Smart Wallet contract.

```yaml
---
description: User-Agent Smart Wallet for managing assets and DAO interactions
---
```

# Smart Wallet

The Smart Wallet provides a secure interface between users and their agents, enabling controlled asset management and DAO participation. It creates a permission structure where users maintain full control of their assets while allowing agents to perform specific actions on their behalf.

## Key Features

- **Self-Custody**: Users maintain exclusive withdrawal rights
- **Agent Delegation**: Controlled permissions for agents to interact with DAOs
- **Asset Management**: Deposit, withdraw, and trade approved assets
- **DAO Governance**: Create, vote on, and conclude proposals
- **Trading Controls**: Optional agent trading with user-defined limits

## Quick Reference

| Property          | Value                                                                          |
| ----------------- | ------------------------------------------------------------------------------ |
| Contract Name     | `aibtc-user-agent-smart-wallet`                                                |
| Version           | 1.0.0                                                                          |
| Implements        | `aibtc-smart-wallet`, `aibtc-proposals-v2`, `faktory-buy-sell`                 |
| Naming Convention | `aibtc-smart-wallet-[OWNER_FIRST5]-[OWNER_LAST5]-[AGENT_FIRST5]-[AGENT_LAST5]` |

## How It Works

```mermaid
flowchart TD
    A["User"]
    B["Agent"]
    C["Smart Wallet"]
    D["DAO Contracts"]
    E["Approved DEXes"]
    
    subgraph User Operations
        CA["Asset Management"]
        CB["Permission Control"]
    end
    
    subgraph Agent Operations
        CC["Governance Actions"]
        CD["Trading Operations"]
    end
    
    A -->|"Deposits assets"| CA
    A -->|"Withdraws assets"| CA
    A -->|"Approves assets/DEXes"| CB
    A -->|"Controls agent permissions"| CB
    B -->|"Proposes actions"| CC
    B -->|"Votes on proposals"| CC
    B -->|"Trades assets if permitted"| CD
    
    CA --> C
    CB --> C
    CC --> C
    CD --> C
    
    C -->|"Interacts with"| D
    C -->|"Trades on"| E
```

The Smart Wallet acts as a secure intermediary, with different permission levels for users and agents. Users maintain full control over assets and configuration, while agents can perform governance actions and (when permitted) trading operations.

## Public Functions

### `deposit-stx`

**Purpose**: Deposits STX into the smart wallet

**Parameters**:

- `amount`: uint - Amount of STX to deposit

**Returns**: (response bool uint) - Success or error code

**Example**:

```clarity
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG deposit-stx u1000000)
```

### `withdraw-stx`

**Purpose**: Withdraws STX from the smart wallet (user only)

**Parameters**:

- `amount`: uint - Amount of STX to withdraw

**Returns**: (response bool uint) - Success or error code

**Example**:

```clarity
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG withdraw-stx u500000)
```

### `vote-on-action-proposal`

**Purpose**: Votes on an action proposal (user or agent)

**Parameters**:

- `action-proposals`: action-proposals-trait - The action proposals contract
- `proposalId`: uint - The proposal ID
- `vote`: bool - True for yes, false for no

**Returns**: (response bool uint) - Success or error code

**Example**:

```clarity
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG vote-on-action-proposal .aibtc-action-proposals-v2 u5 true)
```

## Read-Only Functions

### `get-balance-stx`

**Purpose**: Gets the current STX balance of the smart wallet

**Parameters**: None

**Returns**: uint - Current STX balance

**Example**:

```clarity
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG get-balance-stx)
```

#### `get-configuration`

**Purpose**: Gets the smart wallet configuration

**Parameters**: None

**Returns**: Tuple with user, agent, and other configuration details

**Example**:

```clarity
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG get-configuration)
```

## Print Events

| Event                     | Description                               | Data                                                 |
| ------------------------- | ----------------------------------------- | ---------------------------------------------------- |
| `deposit-stx`             | Emitted when STX is deposited             | Amount, sender, caller, recipient                    |
| `withdraw-stx`            | Emitted when STX is withdrawn             | Amount, sender, caller, recipient                    |
| `vote-on-action-proposal` | Emitted when voting on an action proposal | Proposal contract, proposal ID, vote, sender, caller |

## Integration Examples

### Depositing STX and Voting on a Proposal

```clarity
;; Deposit STX to the smart wallet
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG deposit-stx u1000000)

;; Vote on an action proposal
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG vote-on-action-proposal .aibtc-action-proposals-v2 u5 true)
```

### Agent Trading with Permission

```clarity
;; User enables agent trading
(as-contract
  (contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG set-agent-can-buy-sell true)
)

;; Agent buys tokens
(contract-call? .aibtc-smart-wallet-ST1PQ-PGZGM-ST2CY-RK9AG buy-asset .aibtc-token-dex .aibtc-token u100000000)
```

## Error Handling

| Error Code | Constant                 | Description                              | Resolution                                                       |
| ---------- | ------------------------ | ---------------------------------------- | ---------------------------------------------------------------- |
| u9000      | ERR_UNAUTHORIZED         | Caller is not authorized                 | Ensure you're calling from the correct principal (user or agent) |
| u9001      | ERR_UNKNOWN_ASSET        | Asset is not in the approved list        | Call approve-asset first to add the asset to the approved list   |
| u9002      | ERR_OPERATION_FAILED     | Operation failed                         | Check parameters and try again                                   |
| u9003      | ERR_BUY_SELL_NOT_ALLOWED | Buy/sell operation not allowed for agent | User must call set-agent-can-buy-sell to enable trading          |

## Security Considerations

- **Principal Separation**: User and agent addresses are separate and have different permissions
- **Asset Approval**: Assets must be explicitly approved before they can be used
- **Withdrawal Restrictions**: Only the user can withdraw assets
- **Trading Controls**: Agent trading can be enabled/disabled by the user
- **Immutable Configuration**: User and agent addresses cannot be changed after deployment

## Related Contracts

- **DAO Action Proposals**: The smart wallet can interact with action proposals for voting
- **DAO Core Proposals**: The smart wallet can interact with core proposals for voting
- **Faktory DEX**: The smart wallet can trade on approved DEXes
