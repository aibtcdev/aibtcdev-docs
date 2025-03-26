---
description: >-
  Sample prompts for submitting action proposals to a DAO.
---

# Action Proposal Prompts

## Creating Action Proposals

### Add a Resource for Invoicing

```
Create an action proposal to add a resource for invoicing using the following info:
- Name: Consulting
- Description: The best consulting services
- Price: 100000000 (100 STX in micro-STX)
- URL: (optional) link for the resource
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_ADD_RESOURCE: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-add-resource
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Toggle Resource Status

```
Create an action proposal to toggle the status of a resource using the following info:
- Name: Consulting (must exist first!)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_TOGGLE_RESOURCE: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-toggle-resource
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Allow Asset in Treasury

```
Create an action proposal to allow an asset in the treasury using the following info:
- TOKEN_TO_ALLOW: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.faces-faktory
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_ALLOW_ASSET: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-allow-asset
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Send On-Chain Message

```
Create an action proposal to send a message to all DAO members about XYZ using the following info:
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_SEND_MESSAGE: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-send-message
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Set Account Holder in Timed Vault

```
Create an action proposal to set the account holder in the timed vault using the following info:
- Account holder: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_SET_ACCOUNT_HOLDER: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-set-account-holder
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Set Withdrawal Amount

```
Create an action proposal to set the withdrawal amount in the timed vault using the following info:
- Withdrawal amount: 50000000 (50 STX in micro-STX)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_SET_WITHDRAWAL_AMOUNT: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-set-withdrawal-amount
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

### Set Withdrawal Period

```
Create an action proposal to set the withdrawal period in the timed vault using the following info:
- Withdrwawal period: 4320 (30 days in BTC blocks)
  (also could try something creative, e.g. With 10min BTC blocks set it for 3 days)
- VOTING_EXTENSION: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-proposals-v2
- ACTION_SET_WITHDRAWAL_PERIOD: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-action-set-withdrawal-period
- TOKEN_DAO: ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA.media2-faktory
```

## Full Proposal Walkthrough

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
