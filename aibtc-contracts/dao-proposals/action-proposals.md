---
description: >-
  Action proposals are predefined operations that can be executed with lower
  voting requirements.
---

# Action Proposals

Action proposals are predefined operations that can be executed with lower voting requirements than core proposals. They provide a streamlined way to perform common DAO operations while maintaining appropriate governance controls.

Each action is implemented as a smart contract that executes specific functionality through the DAO's extensions. These actions must be registered as extensions with the base DAO contract before they can be used in action proposal voting.

## Voting Parameters

- **Approval Threshold**: 66% (compared to 80% for core proposals)
- **Quorum Requirement**: 15% (compared to 20% for core proposals)
- **Voting Period**: Same as core proposals

{% hint style="info" %}
Proposals expire and will not execute if not submitted in time. This prevents holding an early proposal and executing it later. The proposal must be executed within 1 voting period following the end block + the voting delay.
{% endhint %}

## Available Actions

### Payment Processor Management

The DAO supports three payment processor extensions, each handling a different token type: DAO tokens, STX, and sBTC. The following actions are available for each payment processor.

#### Add Resource Actions

These actions create new payable resources in the payment processor system:

| Action Contract | Token Type | Description | Parameters |
|-----------------|------------|-------------|------------|
| `aibtc-action-pmt-dao-add-resource` | DAO Token | Creates a resource payable with DAO tokens | name, description, price, url (optional) |
| `aibtc-action-pmt-stx-add-resource` | STX | Creates a resource payable with STX | name, description, price, url (optional) |
| `aibtc-action-pmt-sbtc-add-resource` | sBTC | Creates a resource payable with sBTC | name, description, price, url (optional) |

Each add-resource action:
- Creates a new payable resource with the specified name, description, and price
- Makes the resource available for immediate invoice payment after creation
- Optionally links to additional information via the URL parameter
- Emits an event recording the resource creation

**Example Parameters:**
```
{
  name: "api-access",
  description: "Monthly access to premium API endpoints",
  price: u10000000, // 10 STX, 10M DAO tokens, or 0.0001 BTC depending on variant
  url: "https://docs.example.com/api"
}
```

#### Toggle Resource Actions

These actions enable or disable existing resources in the payment processor:

| Action Contract | Token Type | Description | Parameters |
|-----------------|------------|-------------|------------|
| `aibtc-action-pmt-dao-toggle-resource` | DAO Token | Toggles a DAO token resource | resourceName |
| `aibtc-action-pmt-stx-toggle-resource` | STX | Toggles a STX resource | resourceName |
| `aibtc-action-pmt-sbtc-toggle-resource` | sBTC | Toggles a sBTC resource | resourceName |

Each toggle-resource action:
- Enables a disabled resource or disables an enabled resource
- Controls availability for invoice payments
- Requires the resource name as a parameter
- Emits an event recording the status change

**Example Parameters:**
```
"api-access" // The name of the resource to toggle
```

### Treasury Management

| Action Contract | Description | Parameters |
|-----------------|-------------|------------|
| `aibtc-action-treasury-allow-asset` | Adds or removes an asset from the treasury allowlist | asset (principal) |

The treasury-allow-asset action:
- Adds a fungible token (FT) or non-fungible token (NFT) to the treasury allowlist
- Enables deposits and withdrawals of the asset
- Is required before an asset can be used with the treasury
- Takes the asset contract principal as a parameter

**Example Parameters:**
```
'SP2C2YFP12AJZB4MABJBAJ55XECVS7E4PMMZ89YZR.usda-token // The principal of the asset contract
```

### Timed Vault Configuration

The DAO supports three timed vault extensions, each handling a different token type: DAO tokens, STX, and sBTC. The following actions configure these vaults:

| Action Contract | Token Type | Description | Parameters |
|-----------------|------------|-------------|------------|
| `aibtc-action-configure-timed-vault-dao` | DAO Token | Configures the DAO token timed vault | accountHolder, amount, period (all optional) |
| `aibtc-action-configure-timed-vault-stx` | STX | Configures the STX timed vault | accountHolder, amount, period (all optional) |
| `aibtc-action-configure-timed-vault-sbtc` | sBTC | Configures the sBTC timed vault | accountHolder, amount, period (all optional) |

Each configure-timed-vault action can set one or more of the following parameters:
- **accountHolder**: The principal authorized to make withdrawals
- **amount**: The amount that can be withdrawn in each period
  - DAO token: 100M-1T tokens (u100000000-u1000000000000)
  - STX: 1-100 STX (u1000000-u100000000)
  - sBTC: 0.00001-0.1 BTC (u1000-u10000000)
- **period**: The time between allowed withdrawals (6-8064 blocks, approximately 1 hour to 1 week)

**Example Parameters:**
```
{
  accountHolder: 'SP2C2YFP12AJZB4MABJBAJ55XECVS7E4PMMZ89YZR,
  amount: u10000000, // 10 STX
  period: u144 // ~1 day
}
```

### Messaging

| Action Contract | Description | Parameters |
|-----------------|-------------|------------|
| `aibtc-action-send-message` | Posts a verified DAO message on-chain | message (string) |

The send-message action:
- Posts a verified DAO message on the blockchain
- Includes a DAO verification flag
- Is limited to 1MB size (1,048,576 ASCII characters)
- Takes the message text as a parameter

**Example Parameters:**
```
"The DAO has approved funding for the new development initiative. Work will begin on May 1st."
```

## Creating and Submitting Action Proposals

Action proposals are created and submitted through the DAO's action proposal extension. Here's how to create and submit an action proposal:

### 1. Prepare the Action Parameters

First, prepare the parameters for the action you want to execute. For example, to add a new resource to the STX payment processor:

```clarity
;; Parameters for adding a new resource
(define-data-var params (buff 2048) 
  (to-consensus-buff? {
    name: "api-access",
    description: "Monthly access to premium API endpoints",
    price: u10000000,
    url: (some "https://docs.example.com/api")
  })
)
```

### 2. Submit the Action Proposal

Next, submit the action proposal using the `submit-proposal` function:

```clarity
(contract-call? .aibtc-base-dao submit-proposal
  .aibtc-action-pmt-stx-add-resource ;; The action contract
  (var-get params) ;; The parameters
  none ;; No memo
  u0 ;; No STX transfer
)
```

### 3. Vote on the Proposal

DAO members can then vote on the proposal:

```clarity
(contract-call? .aibtc-base-dao vote-on-proposal
  proposal-id ;; The ID returned from submit-proposal
  true ;; Vote "yes"
)
```

### 4. Execute the Proposal

After the voting period ends and if the proposal passes, it can be executed:

```clarity
(contract-call? .aibtc-base-dao execute-proposal
  proposal-id ;; The ID of the passed proposal
)
```

## Benefits of Action Proposals

Action proposals provide several advantages over core proposals:

1. **Lower Voting Requirements**: Easier to pass for routine operations
2. **Predefined Operations**: Clear constraints on what can be executed
3. **Specialized Functionality**: Tailored for specific common tasks
4. **Reduced Complexity**: Simplified parameter handling
5. **Enhanced Security**: Limited scope reduces risk

By using action proposals for routine operations, the DAO can operate more efficiently while maintaining appropriate governance controls for more significant decisions that require core proposals.
