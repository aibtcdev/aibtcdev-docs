---
description: >-
  Core proposals can execute arbitrary Clarity code within the DAO context,
  requiring higher consensus due to their significant impact.
---

# Core Proposals

Core proposals can execute arbitrary Clarity code within the DAO context, requiring higher consensus due to their significant impact. Each proposal is implemented as a distinct contract that executes functionality through the DAO's extensions.

## Voting Parameters

- **Approval Threshold**: 90% (compared to 66% for action proposals)
- **Quorum Requirement**: 25% (compared to 15% for action proposals)
- **Voting Period**: Defined in the DAO configuration

{% hint style="info" %}
Proposals expire and will not execute if not submitted in time. This prevents holding an early proposal and executing it later. The proposal must be executed within 1 voting period following the end block + the voting delay.
{% endhint %}

## Available Core Proposals

### DAO Configuration

| Proposal Contract | Description | Parameters |
|------------------|-------------|------------|
| `aibtc-base-bootstrap-initialization-v2` | Sets up initial DAO state | extensions, actions, treasury permissions, manifest |
| `aibtc-base-add-new-extension` | Adds and enables a new extension | extension (principal) |
| `aibtc-base-disable-extension` | Disables an existing extension | extension (principal) |
| `aibtc-base-enable-extension` | Enables a previously disabled extension | extension (principal) |
| `aibtc-base-replace-extension` | Replaces an extension with a new version | oldExtension (principal), newExtension (principal) |
| `aibtc-base-replace-extension-proposal-voting` | Updates proposal voting parameters | parameters (various) |
| `aibtc-action-proposals-set-proposal-bond` | Sets the bond required for action proposals | bondAmount (uint) |
| `aibtc-core-proposals-set-proposal-bond` | Sets the bond required for core proposals | bondAmount (uint) |

These proposals manage the fundamental configuration of the DAO, including which extensions are enabled, how proposals are processed, and what bonds are required to submit proposals.

### DAO Charter

| Proposal Contract | Description | Parameters |
|------------------|-------------|------------|
| `aibtc-dao-charter-set-dao-charter` | Updates the DAO's charter | charter (string) |

This proposal allows updating the DAO's charter, which defines its purpose, principles, and governance rules.

### Messaging

| Proposal Contract | Description | Parameters |
|------------------|-------------|------------|
| `aibtc-onchain-messaging-send` | Sends a verified message from the DAO | message (string) |

This proposal allows the DAO to send verified messages that are stored permanently on-chain.

### Payment Processor Management

The DAO supports three payment processor extensions, each handling a different token type: DAO tokens, STX, and sBTC. The following proposals are available for each payment processor.

#### Add Resource Proposals

| Proposal Contract | Token Type | Description | Parameters |
|------------------|------------|-------------|------------|
| `aibtc-pmt-dao-add-resource` | DAO Token | Creates a resource payable with DAO tokens | name, description, price, url (optional) |
| `aibtc-pmt-stx-add-resource` | STX | Creates a resource payable with STX | name, description, price, url (optional) |
| `aibtc-pmt-sbtc-add-resource` | sBTC | Creates a resource payable with sBTC | name, description, price, url (optional) |

#### Toggle Resource Proposals

| Proposal Contract | Token Type | Description | Parameters |
|------------------|------------|-------------|------------|
| `aibtc-pmt-dao-toggle-resource` | DAO Token | Toggles a DAO token resource | resource (principal) |
| `aibtc-pmt-stx-toggle-resource` | STX | Toggles a STX resource | resource (principal) |
| `aibtc-pmt-sbtc-toggle-resource` | sBTC | Toggles a sBTC resource | resource (principal) |
| `aibtc-pmt-dao-toggle-resource-by-name` | DAO Token | Toggles a DAO token resource by name | resourceName (string) |
| `aibtc-pmt-stx-toggle-resource-by-name` | STX | Toggles a STX resource by name | resourceName (string) |
| `aibtc-pmt-sbtc-toggle-resource-by-name` | sBTC | Toggles a sBTC resource by name | resourceName (string) |

#### Set Payment Address Proposals

| Proposal Contract | Token Type | Description | Parameters |
|------------------|------------|-------------|------------|
| `aibtc-pmt-dao-set-payment-address` | DAO Token | Sets the payment receiving address | paymentAddress (principal) |
| `aibtc-pmt-stx-set-payment-address` | STX | Sets the payment receiving address | paymentAddress (principal) |
| `aibtc-pmt-sbtc-set-payment-address` | sBTC | Sets the payment receiving address | paymentAddress (principal) |

These proposals manage the payment processor extensions, allowing the DAO to create, toggle, and configure payment resources and addresses.

### Timed Vault Management

The DAO supports three timed vault extensions, each handling a different token type: DAO tokens, STX, and sBTC. The following proposals are available for each timed vault.

#### Vault Configuration Proposals

| Proposal Contract | Token Type | Description | Parameters |
|------------------|------------|-------------|------------|
| `aibtc-timed-vault-dao-initialize-new-vault` | DAO Token | Initializes a new DAO token vault | parameters (various) |
| `aibtc-timed-vault-stx-initialize-new-vault` | STX | Initializes a new STX vault | parameters (various) |
| `aibtc-timed-vault-sbtc-initialize-new-vault` | sBTC | Initializes a new sBTC vault | parameters (various) |
| `aibtc-timed-vault-dao-set-account-holder` | DAO Token | Sets the authorized withdrawer | accountHolder (principal) |
| `aibtc-timed-vault-stx-set-account-holder` | STX | Sets the authorized withdrawer | accountHolder (principal) |
| `aibtc-timed-vault-sbtc-set-account-holder` | sBTC | Sets the authorized withdrawer | accountHolder (principal) |
| `aibtc-timed-vault-dao-set-withdrawal-amount` | DAO Token | Sets the withdrawal amount | amount (uint) |
| `aibtc-timed-vault-stx-set-withdrawal-amount` | STX | Sets the withdrawal amount | amount (uint) |
| `aibtc-timed-vault-sbtc-set-withdrawal-amount` | sBTC | Sets the withdrawal amount | amount (uint) |
| `aibtc-timed-vault-dao-set-withdrawal-period` | DAO Token | Sets the withdrawal period | period (uint) |
| `aibtc-timed-vault-stx-set-withdrawal-period` | STX | Sets the withdrawal period | period (uint) |
| `aibtc-timed-vault-sbtc-set-withdrawal-period` | sBTC | Sets the withdrawal period | period (uint) |
| `aibtc-timed-vault-dao-override-last-withdrawal-block` | DAO Token | Overrides the last withdrawal block | block (uint) |
| `aibtc-timed-vault-stx-override-last-withdrawal-block` | STX | Overrides the last withdrawal block | block (uint) |
| `aibtc-timed-vault-sbtc-override-last-withdrawal-block` | sBTC | Overrides the last withdrawal block | block (uint) |

#### Withdrawal Proposals

| Proposal Contract | Token Type | Description | Parameters |
|------------------|------------|-------------|------------|
| `aibtc-timed-vault-dao-withdraw` | DAO Token | Triggers a DAO token withdrawal | amount (uint) |
| `aibtc-timed-vault-stx-withdraw` | STX | Triggers an STX withdrawal | amount (uint) |
| `aibtc-timed-vault-sbtc-withdraw` | sBTC | Triggers an sBTC withdrawal | amount (uint) |

These proposals manage the timed vault extensions, allowing the DAO to configure withdrawal rules, set account holders, and trigger withdrawals.

### Token Management

| Proposal Contract | Description | Parameters |
|------------------|-------------|------------|
| `aibtc-token-owner-transfer-ownership` | Transfers token contract ownership | newOwner (principal) |
| `aibtc-token-owner-set-token-uri` | Updates the token URI metadata | uri (string) |

These proposals manage the DAO token configuration, allowing the DAO to update token metadata and transfer ownership.

### Treasury Operations

| Proposal Contract | Description | Parameters |
|------------------|-------------|------------|
| `aibtc-treasury-withdraw-stx` | Withdraws STX from treasury | amount (uint), recipient (principal) |
| `aibtc-treasury-withdraw-ft` | Withdraws fungible tokens from treasury | ft (principal), amount (uint), recipient (principal) |
| `aibtc-treasury-withdraw-nft` | Withdraws non-fungible tokens from treasury | nft (principal), id (uint), recipient (principal) |
| `aibtc-treasury-allow-asset` | Adds an asset to the treasury allowlist | asset (principal), enabled (bool) |
| `aibtc-treasury-allow-assets` | Adds multiple assets to the treasury allowlist | allowList (list of {token, enabled}) |
| `aibtc-treasury-disable-asset` | Removes an asset from the treasury allowlist | asset (principal) |
| `aibtc-treasury-delegate-stx` | Delegates STX for stacking | maxAmount (uint), to (principal) |
| `aibtc-treasury-revoke-delegation` | Revokes STX delegation | none |

These proposals manage the treasury extension, allowing the DAO to withdraw assets, manage the asset allowlist, and control STX stacking delegation.

## Creating and Submitting Core Proposals

Core proposals are created and submitted through the DAO's core proposal extension. Here's how to create and submit a core proposal:

### 1. Deploy the Proposal Contract

First, deploy the proposal contract that implements the functionality you want to execute:

```clarity
;; Example proposal contract to withdraw STX from treasury
(impl-trait .aibtcdev-dao-traits-v1.proposal)

(define-public (execute (sender principal))
  (begin
    (try! (contract-call? .aibtc-treasury withdraw-stx u1000000 'SP2C2YFP12AJZB4MABJBAJ55XECVS7E4PMMZ89YZR))
    (ok true)
  )
)
```

### 2. Submit the Core Proposal

Next, submit the core proposal using the `submit-proposal` function:

```clarity
(contract-call? .aibtc-base-dao submit-proposal
  .my-custom-proposal ;; The deployed proposal contract
  none ;; No parameters needed as they're hardcoded in the proposal
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

## Creating Custom Core Proposals

Any contract that:

1. Implements the proposal trait (`aibtcdev-dao-traits-v1.proposal`)
2. Makes valid calls to enabled extensions
3. Can be executed through the base DAO

Can be proposed as a core proposal. This allows for unlimited extensibility while maintaining security through high voting thresholds.

Custom proposals can combine multiple operations, include conditional logic, or implement entirely new functionality as long as they work through the DAO's extension system.

## Benefits of Core Proposals

Core proposals provide several advantages:

1. **Maximum Flexibility**: Can execute any operation supported by the DAO's extensions
2. **Complex Operations**: Can combine multiple operations in a single proposal
3. **Custom Logic**: Can include conditional logic and error handling
4. **Future-Proofing**: Allows the DAO to adapt to new requirements without changing its core structure
5. **Strong Security**: Higher voting thresholds ensure significant consensus for impactful changes

By using core proposals for significant decisions and complex operations, the DAO can maintain both flexibility and security in its governance system.
