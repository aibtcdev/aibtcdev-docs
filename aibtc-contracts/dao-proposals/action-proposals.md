---
description: >-
  Action proposals, managed by the aibtc-action-proposal-voting contract, are predefined operations that can be executed with specific voting requirements.
---

# Action Proposals

Action proposals, managed by the `aibtc-action-proposal-voting` contract (version 3.0.0), allow DAO members to propose and vote on predefined actions. These actions are separate smart contracts that implement the `.aibtc-dao-traits.action` trait and must be registered with the DAO. Action proposals provide a streamlined way to perform common DAO operations, with an initial focus on enabling on-chain messaging.

## Voting Parameters & Lifecycle

Action proposals follow a specific lifecycle with defined parameters:

-   **Approval Threshold**: 66% of votes cast must be in favor (`VOTING_THRESHOLD`).
-   **Quorum Requirement**: 15% of the liquid DAO token supply must participate in voting (`VOTING_QUORUM`).
-   **Initial Voting Delay (`VOTING_DELAY`)**: A period after proposal creation before voting can begin (e.g., ~1 day or 144 Stacks blocks).
-   **Voting Period (`VOTING_PERIOD`)**: The duration during which DAO members can cast their votes (e.g., ~2 days or 288 Stacks blocks).
-   **Veto Period / Execution Delay (`VOTING_DELAY`)**: A period after voting ends, equal to the initial voting delay, during which token holders can cast veto votes against a passed proposal.
-   **Execution Window (`VOTING_PERIOD`)**: A period after the veto period, equal to the voting period, during which a passed, non-vetoed proposal can be concluded and its action executed.

{% hint style="info" %}
**Proposal Expiry**: A proposal must be concluded by calling `conclude-action-proposal` after its veto period has ended (`execStart`) and before its execution window closes (`execEnd`). If not concluded within this window, the proposal expires and cannot be executed.
{% endhint %}

## Key Financials and Mechanisms

The `aibtc-action-proposal-voting` contract introduces several mechanisms:

-   **Proposal Bond (`VOTING_BOND`)**:
    *   Proposers must lock a bond (e.g., 5,000 DAO tokens) when creating a proposal.
    *   The bond is held by the `aibtc-action-proposal-voting` contract.
    *   It's returned to the proposer if the proposal passes, is not vetoed, and the action executes successfully.
    *   It's forfeited to the DAO treasury (`.aibtc-treasury`) if the proposal fails, is vetoed, or if the action execution fails.
-   **DAO Run Cost (`AIBTC_DAO_RUN_COST_AMOUNT`)**:
    *   Proposers must have sufficient balance to cover a non-refundable fee (e.g., 100 DAO tokens) that contributes to DAO operational costs.
    *   This fee is transferred from the `.aibtc-treasury` to the `.aibtc-dao-run-cost` contract upon proposal creation, facilitated by the `aibtc-action-proposal-voting` contract.
-   **Proposal Reward (`VOTING_REWARD`)**:
    *   A reward (e.g., 1,000 DAO tokens) is set aside from the `.aibtc-treasury` into the `.aibtc-rewards-account` when a proposal is created.
    *   If the proposal passes, is not vetoed, and the action executes successfully, the reward is transferred from `.aibtc-rewards-account` to the proposer.
    *   If the proposal fails, is vetoed, or the action execution fails, the reward is returned from `.aibtc-rewards-account` to the `.aibtc-treasury`.
-   **Veto Mechanism**:
    *   Allows token holders to prevent a passed proposal from being executed.
    *   Veto votes can be cast during the Veto Period (Execution Delay).
    *   A successful veto requires meeting a quorum and having veto votes exceed 'yes' votes.
-   **Reputation Adjustments**:
    *   The proposal creator's reputation score in the `.aibtc-dao-users` extension is increased for successful proposals and decreased for failed ones.
-   **Liquid Supply Snapshot**:
    *   Voting power is determined by a voter's DAO token balance at the Stacks block height when the proposal was created (`createdStx`), ensuring fairness.

## Available Actions (Initial Focus)

Version 3.0.0 of `aibtc-action-proposal-voting` primarily enables proposals for the `.aibtc-onchain-messaging` contract. While the system is designed to support various actions (any contract implementing `.aibtc-dao-traits.action` and registered with the DAO), this documentation will focus on the messaging action.

### On-Chain Messaging

| Action Contract             | Target Function | Description                                     | Parameters (for `send` function) |
| --------------------------- | --------------- | ----------------------------------------------- | -------------------------------- |
| `.aibtc-onchain-messaging` | `send`          | Posts a verified DAO message on-chain.          | `msg (string-ascii 10000)`       |

The `.aibtc-onchain-messaging.send` action:
-   Posts a message (up to 10,000 ASCII characters) that is emitted as a `print` event.
-   The event includes metadata indicating if the message originated from the DAO (via an extension like this one) or a token holder.
-   Provides a transparent and immutable way for the DAO to make official announcements or communications.

**Example Parameters for `.aibtc-onchain-messaging.send`:**
The `parameters` argument for `create-action-proposal` must be a `(buff 2048)` containing the ABI-encoded parameters for the target action function. For `(send (msg (string-ascii 10000)))`, this is the string message itself, properly encoded.

```clarity
;; Example: Message content
(define-constant MESSAGE_CONTENT "Official DAO Announcement: Q3 Roadmap Update now available on our blog.")

;; The parameters buffer for .aibtc-onchain-messaging.send(MESSAGE_CONTENT)
;; For a single string parameter, direct consensus serialization can often work.
;; For more complex functions, a dedicated ABI encoding tool or helper contract might be necessary.
(define-constant ACTION_PARAMETERS (to-consensus-buff? MESSAGE_CONTENT))
```

## Creating and Submitting Action Proposals

Action proposals are managed by the `.aibtc-action-proposal-voting` contract. Here's the general workflow:

### 1. Prepare the Action and its Parameters

Identify the action contract (e.g., `.aibtc-onchain-messaging`) and prepare the `(buff 2048)` for its parameters.

```clarity
;; Define the action contract and message
(define-constant TARGET_ACTION_CONTRACT .aibtc-onchain-messaging)
(define-constant MESSAGE_TO_SEND "Proposal for funding community grants Q4 2025.")

;; Prepare the parameters buffer for .aibtc-onchain-messaging.send(MESSAGE_TO_SEND)
;; IMPORTANT: Ensure this is correctly ABI-encoded for the target function.
(define-constant ACTION_PARAMS (to-consensus-buff? MESSAGE_TO_SEND))
```

### 2. Create the Action Proposal

Call `create-action-proposal` on the `.aibtc-action-proposal-voting` contract. The caller must have enough DAO tokens (`.aibtc-faktory`) to cover the `VOTING_BOND` plus the `AIBTC_DAO_RUN_COST_AMOUNT`.

```clarity
(contract-call? .aibtc-action-proposal-voting create-action-proposal
  TARGET_ACTION_CONTRACT ;; The action contract principal, e.g., .aibtc-onchain-messaging
  ACTION_PARAMS          ;; The (buff 2048) of ABI-encoded parameters
  (some "Proposal to announce Q4 community grants.") ;; Optional memo (string-ascii 1024)
)
;; This call will return (ok true) on success of the transaction.
;; The proposal ID is generated internally and can be found in the emitted event
;; or by querying (get-total-proposals) on the aibtc-action-proposal-voting contract.
```

### 3. Vote on the Proposal

During the `VOTING_PERIOD` (after `VOTING_DELAY`), DAO token holders can vote. Voting power is based on their balance at the proposal's creation block.

```clarity
(contract-call? .aibtc-action-proposal-voting vote-on-action-proposal
  u1        ;; The proposal ID
  true      ;; Vote 'yes' (true) or 'no' (false)
)
```

### 4. (Optional) Veto the Proposal

During the Veto Period (after `VOTING_PERIOD` ends and before `execStart`), token holders can cast veto votes.

```clarity
(contract-call? .aibtc-action-proposal-voting veto-action-proposal
  u1        ;; The proposal ID to veto
)
```

### 5. Conclude the Proposal

After the Veto Period ends (i.e., at or after `execStart`) and before `execEnd`, anyone can call `conclude-action-proposal`. This function finalizes the proposal:
- Tallies votes and checks against quorum/threshold.
- Checks for successful veto.
- If passed, not vetoed, and not expired, it attempts to execute the action.
- Distributes the bond and reward accordingly.

```clarity
(contract-call? .aibtc-action-proposal-voting conclude-action-proposal
  u1                       ;; The proposal ID
  TARGET_ACTION_CONTRACT   ;; The action contract principal (must match the one in the proposal)
)
;; Returns (ok true) if action executed successfully, (ok false) if proposal passed but action failed,
;; or if proposal did not pass/was vetoed/expired. Returns an error for other issues.
```

## Benefits of Action Proposals

Action proposals, as managed by `aibtc-action-proposal-voting`, offer several advantages:

1.  **Defined Voting Requirements**: Clear and specific voting parameters suitable for routine or predefined operations.
2.  **Predefined and Vetted Actions**: Actions are specific contracts, limiting the scope of what can be executed and allowing for focused security reviews.
3.  **Streamlined Process**: A clear lifecycle with defined periods for voting, veto, and execution.
4.  **Incentivized Participation**: Proposal bonds, run costs, and rewards encourage thoughtful proposals and discourage spam.
5.  **Enhanced Security through Veto**: The veto mechanism provides an additional safeguard against contentious or potentially harmful proposals.
6.  **Transparency**: All proposal details, votes, and outcomes are recorded on-chain.

By using action proposals for suitable operations, the DAO can operate more efficiently while maintaining robust governance and security.
