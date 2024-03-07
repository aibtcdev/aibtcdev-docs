---
description: A simple decentralized on-chain invoicing primitive.
---

# Resource Contracts

## Overview

When we pay for services online or in-person, the payment is generally disconnected from the service that's provided. The payment itself is routed through a payment processor (credit cards, PayPal, Stripe, etc), which provides verification of who paid what, when they paid, and what they subscribed to.

The service provider now relies on the payment processor in order to operate, and a lot of software integrations exist now as a result, so that a service provider can keep track of their customers, recent payments, and service obligations.

{% hint style="info" %}
What if we could achieve the same outcome through a smart contract instead of a payment processor? That's where the resource contract comes in!
{% endhint %}

## Resource Contract

Anyone can deploy a resource smart contract, which is a payment primitive that allows someone to create and offer resources for a defined price, and allows anyone to pay for them with a smart contract function call.

The contract provides the following features.

### **Trait Specification**

A [Clarity trait specification](https://book.clarity-lang.org/ch09-00-traits.html) is used with each resource contract to allow querying [all contracts with the same signature](https://docs.hiro.so/api/get-contracts-by-trait), which is critical to having an aggregate view of all resource contracts.

This also allows for other contracts to implement a dynamic inter-contract calls if needed.

### **Resources**

Resources are the core concept in the contract, and represent a service provided by the contract deployer.

Resources are uniquely defined by name and given an index, and the contract tracks the total number of resources available as well as data for each.

For each resource, the following data is tracked in the contract:

* **createdAt:** block height the resource was created
* **enabled:** true by default, flag to disable if no longer offered, setting to false will cause any invoice payments to fail for this resource as a fail-safe
* **name:** 50-char string describing the resource
* **description:** 255-char string for proving additional information about the resource
* **price:** cost of each resource invoice, denominated in aiBTC on testnet, preparing for xBTC/aBTC/sBTC on mainnet
  * note: aiBTC amounts are often denoted in sats, e.g. `amount * 10_000_000`
  * note: you can get aiBTC from the testnet faucet functions in the aiBTC token contract
* **totalSpent:** total aiBTC spent on this resource
* **totalUsed:** total times this resource was paid for

### **Users**

Users represent any address (principal) that interacts with the smart contract through a public function call. This can be a user (standard principal) or another smart contract (contract principal).

Users are uniquely defined by their address and given an index, and the contract tracks the total number of users available as well as data for each.

For each user, the following data is tracked in the contract:

* **address:** address for the given user index
* **totalSpent:** total aiBTC spent by the user
* **totalUsed:** total times the user paid for a resource

### Invoices

Invoices represent a payment record for a resource by a user, connecting the two concepts and allowing easy look up of recent payment data.

Invoices are uniquely defined by an index which increases with each invoice paid in the smart contract, and the contract tracks the total number of invoices as well as data for each.

For each invoice, the following data is tracked in the contract:

* **amount:** amount paid by the user for the resource, determined by resource price
* **createdAt:** block height the invoice was created
* **userIndex:** user index of the payee, for easy data lookup
* **resourceName:** resource name, showing what the user paid for
* **resourceIndex:** resource index, for easy data lookup

### Recent Payments

A common question when providing a service is "when did the user last pay?" The contract provides an easy lookup for this by tracking the last payment for a user separately from the invoice index.

Recent payments are uniquely defined by a user and a resource, and return a reference to the invoice index for easy data lookup in the contract.

Using this information we can decide **from on-chain data** if the user is eligible for a service based on our own criteria as a service provider, providing an easy way to check what the user paid for and when they paid for it.

