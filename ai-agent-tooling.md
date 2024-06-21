---
description: Connecting AI agents to the blockchain.
---

# AI Agent Tooling

## Overview

Large language models are excellent for having conversations, but when we want them to complete tasks it becomes imperative to equip AI agents with the correct tools.

The current infrastructure for agent tooling (through [CrewAI](https://docs.crewai.com/core-concepts/Tools/) or [Langchain](https://python.langchain.com/docs/modules/agents/tools/)) generally accepts one parameter, so a critical approach to creating new tools is to take inspiration from the [UNIX philosophy:](https://en.wikipedia.org/wiki/Unix\_philosophy#Do\_One\_Thing\_and\_Do\_It\_Well)

1. **Make each program do one thing well.** To do a new job, build afresh rather than complicate old programs by adding new "features".
2. **Expect the output of every program to become the input to another**, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input.
3. **Design and build software, even operating systems, to be tried early**, ideally within weeks. Don't hesitate to throw away the clumsy parts and rebuild them.
4. **Use tools in preference to unskilled help to lighten a programming task**, even if you have to detour to build the tools and expect to throw some of them out after you've finished using them.

## Agent Tooling

Agent tools can be any python function with the following criteria:

* created with the BaseTool class or marked with `@tool` decorator
* contains a clear function name and docstring description
* only accepts one input (can be no input as a dummy arg)
* returns useful data for the AI agent to work with based on the query
* returns an error message that helps the AI agent make a successful call a second time

The current agent tools are located in the [agent-tools-ts repository](https://github.com/aibtcdev/agent-tools-ts), with a class defined for each category to help group relevant tools together.

The crews and agents that are created in the [ai-agent-crew repository](https://github.com/aibtcdev/ai-agent-crew) import and use the tools from the repository above through git submodules.&#x20;

{% hint style="info" %}
There is a balance between the number of tools available to an agent and how efficiently it will use them. Scoping the agent's role/backstory to the specific tools they will use is helpful in getting consistency.\
\
**Function names, descriptions, and context are key in getting the expected results!**
{% endhint %}

## Stacks.js Integration

The [Stacks.js packages](https://stacks.js.org) are in Typescript and in order to use them with agents [Bun.js](https://bun.sh) is required.

The [example environment file](https://github.com/aibtcdev/agent-tools-ts/blob/main/.env.example) shows how you can create an `.env` file that defines the network, seed phrase, and account index for the agent to use.

{% hint style="info" %}
The [agent-tools-ts](https://github.com/aibtcdev/agent-tools-ts) repository is imported into the [ai-agent-crew](https://github.com/aibtcdev/ai-agent-crew) repository as a submodule. Instructions to clone/update the repository with a submodule and set the required environment variables is included in the [README](https://github.com/aibtcdev/ai-agent-crew?tab=readme-ov-file#setting-up-the-wallet).
{% endhint %}

Using Bun, we can simply run a script from the [agent-tools-ts](https://github.com/aibtcdev/agent-tools-ts) and get a response, e.g.

```sh
$ bun run src/wallet/get-wallet-status.ts

Account index: 0
Account address: ST2HQ5J6RP8HSQE9KKGWCHW9PT9SVE4TDGBZQ3EKR
Nonce: 44
```

The script's output is simply what's printed to the console, and the results are passed back to the requesting agent [through a helper function:](https://github.com/aibtcdev/ai-agent-crew/blob/main/tools/bun\_runner.py)

````python
```python
import subprocess

class BunScriptRunner:
    working_dir = "./agent-tools-ts/"
    script_dir = "src"

    @staticmethod
    def bun_run(contract_name: str, script_name: str, arg: str = None):
        """Runs a TypeScript script using bun with an optional positional argument."""
        command = [
            "bun",
            "run",
            f"{BunScriptRunner.script_dir}/{contract_name}/{script_name}",
        ]

        # Append the optional argument if provided
        if arg is not None:
            command.append(arg)

        try:
            result = subprocess.run(
                command,
                check=True,
                text=True,
                capture_output=True,
                cwd=BunScriptRunner.working_dir,
            )
            return {"output": result.stdout, "error": None, "success": True}
        except subprocess.CalledProcessError as e:
            return {"output": None, "error": e.stderr, "success": False}
```

````

The helper function can also pass a single positional argument, allowing the LLM to specify one parameter to the script.
