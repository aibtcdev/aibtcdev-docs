---
description: Welcome to the Bitcoin x AI working group!
---

# Introduction

## Overview

We are developing primitives for integrating L2 Bitcoin into resources and tools that expand the capabilities of AI agents.

### CrewAI Agent Framework

We use the [CrewAI Agent Framework](https://www.crewai.io/) which enables the following key concepts:

* **agents:** individual AI agents with a role, backstory, and tools
* **tools:** functions available to the agent while completing a task
* **tasks:** assignments the agent should complete and expected output
* **crew:** a group of agents that complete a list of tasks and provide a final result

### Stacks.js SDK

We also use the [Stacks.js SDK](https://docs.hiro.so/stacks.js) for interacting with wallets, smart contracts, and on-chain data.

* For agents, wallet and on-chain tools are provided through [Bun.js scripts](https://bun.sh/) in the **agent-tools-ts** repository which are accessible through a Python runner.
* For the API example, [Stacks.js packages](https://stacks.js.org) are used for reading and responding to on-chain data, as well as encoding/decoding digital signatures.
* The SDK provides options for integrations **with or without private key access**, including several tools to interact with popular wallet extensions like [Leather](https://leather.io) and [Xverse](https://xverse.app) as well as operate with direct CLI access (how agent tooling works now).

## Resources

* [Main Website](https://aibtc.dev)
* [GitHub Discussions](https://github.com/orgs/stacks-network/discussions/categories/bitcoin-x-ai)
* [RSVP Thursdays](https://evt.to/emamdeggw)

## Repositories

[Main GitHub Organization: aibtcdev](https://github.com/aibtcdev)

| Name                                                           | Description                                                                          |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [agent-tools-ts](https://github.com/aibtcdev/agent-tools-ts)   | TS scripts for interacting with the Stacks blockchain, powered by Bun and Stacks.js. |
| [ai-agent-crew](https://github.com/aibtcdev/ai-agent-crew)     | Langchain + CrewAI powered AI agents with Bitcoin wallets.                           |
| [gated-402-api](https://github.com/aibtcdev/gated-402-api)     | Example API implementation with HTTP 402 responses for unpaid resources.             |
| [protocol-docs](https://github.com/aibtcdev/protocol-docs)     | Documentation for using CrewAI AI agents with a Bitcoin wallet.                      |
| [landing-page](https://github.com/aibtcdev/landing-page)       | Main landing page for https://aibtc.dev                                              |
| [smart-contracts](https://github.com/aibtcdev/smart-contracts) | Stacks smart contracts, test suite, and deployment plans.                            |
