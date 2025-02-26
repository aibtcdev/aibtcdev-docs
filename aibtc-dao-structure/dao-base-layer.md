---
description: Built on the ExecutorDAO framework.
---

# DAO Base Layer

The [ExecutorDAO design](https://github.com/MarvinJanssen/executor-dao) is built in Clarity and is very modular and flexible. The key elements are:

* proposals are smart contract and can be executed
* the core executes, the extensions give form
* ownership control happens via sending context

Our [implementation for AIBTC DAOs](https://github.com/aibtcdev/aibtcdev-contracts) adds several ready-to-use extensions with the goal that a DAO can go from idea to fully-functioning on-chain entity.

The built-in proposal voting is based on the DAO's token, and the repo includes several proposal templates and pre-defined actions.
