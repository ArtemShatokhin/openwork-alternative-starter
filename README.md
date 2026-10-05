# Kortix Starter: an Open-Source OpenWork Alternative for Teams

Kortix is open source. It is the AI Management System a team adopts when it outgrows a desktop agent, and this repository is the hands-on starter for that move. It covers the install, a first project, and the review gate where agent work lands.

## What OpenWork is

OpenWork is a free, open-source desktop app for macOS, Windows, and Linux where AI agents do work on files on your own computer. OpenWork is built on OpenCode and runs local-first, so no account is needed to use it locally. It supports any model across 50+ providers through your own API keys, a ChatGPT sign-in, or local models via Ollama, and teammates can share skills and MCP servers. The desktop app and core are MIT licensed, and the organization control plane, OpenWork Den, is published under the OpenWork EE License ([OpenWork on GitHub](https://github.com/different-ai/openwork), checked October 2026).

## Why teams move to Kortix

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. A desktop agent serves one person on one machine. Kortix runs the agents, the skills they share, your company memory, and every connector as one system the company owns.

The differences that matter at team scale:

- **One git repo is the company.** Agents, skills, memory, connector config, and triggers are files in one repo you can grep, diff, and roll back.
- **Every session gets its own computer.** Each session runs on an isolated Linux machine on its own branch, thousands in parallel on the same config.
- **A human gate on every change.** Agent work lands as a change request you read as a diff before it merges to the default branch.
- **Any model, your keys.** Pick the model per agent, per session, or per message, including your own OpenAI-compatible endpoint.
- **Every tool the company runs on.** 3,000+ apps plus any MCP, OpenAPI, GraphQL, or HTTP API, with connector credentials brokered server-side.
- **Self-host or managed cloud.** Run it on your laptop, a VPS, your VPC, or on-prem, or use Kortix Cloud.

Kortix is open source (Elastic License 2.0): self-host, read and modify the code.

## Quickstart: three commands

```bash
# 1. Install the CLI
curl -fsSL https://kortix.com/install | bash

# 2. Scaffold a project: creates kortix.yaml plus your agents, skills, and runtime config
kortix init

# 3. Ship it: pushes your repo and brings the whole thing live
kortix ship
```

Then start your first session and review what it proposes:

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls   # review what the agent proposes, merge to keep it
kortix chat    # talk to a session's agent from your terminal
```

If you would rather skip setup, sign up at [kortix.com](https://kortix.com), create a project, and start a session with nothing to install.

## What's in this repo

- [docs/setup.md](docs/setup.md): install, scaffold a project, the `kortix.yaml` manifest, run a session, review a change request, and self-host your own instance.
- [docs/vs-openwork.md](docs/vs-openwork.md): Kortix and OpenWork side by side for a team deciding between a desktop agent and a company system.
- [docs/faq.md](docs/faq.md): ownership, self-hosting, models, human review, connectors, and cost.

## Links

- Kortix: https://kortix.com
- Documentation: https://kortix.com/docs
- [Kortix on GitHub](https://github.com/kortix-ai/suna)
- Campaign site: https://openworkalternative.com
