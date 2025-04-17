---
description: >-
  Sample prompts for submitting action proposals to a DAO.
---

# Action Proposal Prompts

This document provides sample prompts for creating and managing action proposals in a DAO. Action proposals are predefined operations that can be executed with lower voting requirements (66% approval, 15% quorum) compared to core proposals.

## Creating Action Proposals

### Payment Processor Management

#### Add Resource (DAO Token)

```
Create an action proposal to add a resource payable with DAO tokens using the following info:
- Name: Consulting
- Description: Professional consulting services for blockchain projects
- Price: 100000000 (100M DAO tokens)
- URL: https://docs.example.com/consulting
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-dao-add-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Add Resource (STX)

```
Create an action proposal to add a resource payable with STX using the following info:
- Name: API-Access
- Description: Monthly access to premium API endpoints
- Price: 10000000 (10 STX in micro-STX)
- URL: https://api.example.com/docs
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-stx-add-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Add Resource (sBTC)

```
Create an action proposal to add a resource payable with sBTC using the following info:
- Name: Premium-Support
- Description: Priority technical support for enterprise clients
- Price: 1000 (0.00001 BTC in sats)
- URL: https://support.example.com/premium
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-sbtc-add-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Toggle Resource (DAO Token)

```
Create an action proposal to toggle a DAO token resource using the following info:
- Resource Name: Consulting
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-dao-toggle-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Toggle Resource (STX)

```
Create an action proposal to toggle an STX resource using the following info:
- Resource Name: API-Access
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-stx-toggle-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Toggle Resource (sBTC)

```
Create an action proposal to toggle an sBTC resource using the following info:
- Resource Name: Premium-Support
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-pmt-sbtc-toggle-resource
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

### Treasury Management

#### Allow Asset

```
Create an action proposal to allow an asset in the treasury using the following info:
- Asset Contract: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.usda-token
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-treasury-allow-asset
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

### Timed Vault Configuration

#### Configure DAO Token Vault

```
Create an action proposal to configure the DAO token timed vault using the following info:
- Account Holder: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA
- Withdrawal Amount: 500000000 (500M DAO tokens)
- Withdrawal Period: 144 (approximately 1 day in blocks)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-configure-timed-vault-dao
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Configure STX Vault

```
Create an action proposal to configure the STX timed vault using the following info:
- Account Holder: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA
- Withdrawal Amount: 50000000 (50 STX)
- Withdrawal Period: 144 (approximately 1 day in blocks)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-configure-timed-vault-stx
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

#### Configure sBTC Vault

```
Create an action proposal to configure the sBTC timed vault using the following info:
- Account Holder: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA
- Withdrawal Amount: 5000 (0.00005 BTC)
- Withdrawal Period: 144 (approximately 1 day in blocks)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-configure-timed-vault-sbtc
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

### Messaging

#### Send On-Chain Message

```
Create an action proposal to send a verified message from the DAO using the following info:
- Message: "The DAO has approved funding for the new development initiative. Work will begin on May 1st."
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
- ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-send-message
- BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
```

## Full Proposal Walkthrough

Here's a complete walkthrough for creating and managing an action proposal:

1. **Check wallet balance**

   ```
   Check your wallet balance and report the balances of STX and DAO tokens.
   ```

2. **Get testnet STX (if needed)**

   ```
   Fund my wallet with STX from the testnet faucet.
   ```

3. **Get DAO tokens to participate**

   ```
   Execute a buy order for DAO tokens with the following details:
   - stx_amount: 100000000 (100 STX)
   - dao_token_contract: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-token
   ```

4. **Create an action proposal**

   ```
   Create an action proposal to send the following message from the DAO:
   "We're excited to announce our new partnership with XYZ Protocol. This collaboration will enhance our cross-chain capabilities."
   
   - VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
   - ACTION_CONTRACT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-send-message
   - BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
   ```

5. **Get proposal information**

   ```
   Get the details of my recently submitted proposal, including:
   - Proposal ID
   - Start and end blocks
   - Voting parameters (approval threshold and quorum)
   - Current voting status
   ```

6. **Vote on the proposal**

   ```
   Vote YES on proposal #12 with the following details:
   - VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
   - BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
   - Amount of tokens to vote with: 10000000 (10M tokens)
   ```

7. **Check proposal status**

   ```
   Check the current status of proposal #12, including:
   - Total votes for and against
   - Current approval percentage
   - Whether quorum has been reached
   - Time remaining until voting ends
   ```

8. **Execute the proposal**

   ```
   Execute proposal #12 now that voting has concluded and it has passed:
   - VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-action-proposals-v2
   - BASE_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.aibtc-base-dao
   ```

9. **Verify execution**

   ```
   Verify that proposal #12 was successfully executed by checking:
   - Transaction status
   - On-chain message record
   - DAO activity log
   ```
