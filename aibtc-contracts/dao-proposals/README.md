---
description: Submit proposals, vote on them, and execute if they pass.
---

# DAO Proposals

The DAO is governed entirely by token holders through a proposal system. Currently, this is primarily facilitated through Action Proposals, which are used for predefined operations.

### Overview

All proposals follow a similar lifecycle:

1. Creation - A token holder creates a proposal
2. Voting Period - Token holders cast votes for/against
3. Conclusion - After voting ends, anyone can conclude the proposal
4. Execution - If passed, the proposal automatically executes

### Proposal Types

#### Action Proposals

Action proposals, managed by the `aibtc-action-proposal-voting` extension, are predefined operations that can be executed with lower voting requirements. These are used for routine operations within set parameters, such as sending on-chain messages.

**Voting Parameters (as per `aibtc-action-proposal-voting` v3.0.0):**

*   **Approval Threshold**: 66% of votes in favor.
*   **Quorum Requirement**: 15% of liquid token supply must participate.
*   **Initial Voting Delay**: ~1 day (e.g., 144 Stacks blocks) before voting starts.
*   **Voting Period**: ~2 days (e.g., 288 Stacks blocks) for casting votes.
*   **Veto Period (Execution Delay)**: ~1 day (e.g., 144 Stacks blocks) after voting ends, during which proposals can be vetoed.
*   **Execution Window**: ~2 days (e.g., 288 Stacks blocks) after the veto period, during which a passed and non-vetoed proposal can be concluded and executed.
*   **Proposal Bond**: Required from the proposer, returned on successful execution or forfeited.
*   **DAO Run Cost**: A fee paid by the proposer towards DAO operational costs.
*   **Proposer Reward**: Awarded to the proposer for successfully executed proposals.
