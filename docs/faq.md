# OpenWork Alternative FAQ: Open-Source Kortix for Teams

Kortix is open source, and these are the questions a team asks when it compares Kortix with OpenWork. Each answer stands on its own.

## Does the company own the agents, skills, and memory?

Yes. In Kortix, agents, skills, company memory, connector config, and triggers are text files in one git repo the company owns. You can grep the whole company, diff any change, and roll one part back. Nothing important lives in a vendor's database, so the configuration moves with you. Read more in the [setup guide](setup.md).

## Can we self-host Kortix?

Yes. Kortix self-hosts for free as one Docker Compose stack: the frontend, the API, the LLM gateway, and a Supabase distribution. Run it on a laptop, a VPS, your VPC, or on-prem, or use Kortix Cloud. Agent sessions run on a separate sandbox provider, with Daytona as the default and Platinum and E2B also supported.

## Can we use the models we already pay for?

Yes. Kortix is model-agnostic. Bring an API key from any major provider, sign in with the ChatGPT subscription you already pay for, or point an agent at your own OpenAI-compatible endpoint. The model is chosen per agent, per session, or per message, so you can switch the day a better one lands without rebuilding anything.

## How does human review work?

Every session runs on its own branch, and work reaches the default branch only through a change request a person approves. Merge is default-deny for agents, so you read the diff first. You can also set each tool call to allow, ask, or block, down to the arguments of a single call. An ask holds the call until someone approves it.

## Which tools and connectors can agents reach?

Kortix reaches 3,000+ apps plus any MCP, OpenAPI, GraphQL, or HTTP API. Connector credentials are brokered server-side and never enter the session machine. You scope which agent may touch which connector, and per-call rules decide what runs, what waits for a person, and what is blocked.

## What is the cost model?

Self-hosting Kortix is free, and the code is open source. The managed Kortix Cloud is priced per seat plus usage, published at [kortix.com/pricing](https://kortix.com/pricing). There is no charge for reading or forking the code. Check the pricing page for current figures before you commit to a plan.

## Is OpenWork enough for a small team?

OpenWork is enough when a small team works from its own machines and only needs shared skills and MCP servers. It suits a person or small team that wants a free point-and-click desktop app with files staying local. Kortix is the better fit once the team needs shared agents on cloud computers, one repo for the whole configuration, connectors to company systems, and a human approval gate on every change.

## How do we move from OpenWork to Kortix?

Start with one job and one agent. Keep the skills and MCP connections your team already built, model them as files in the Kortix repo, and point the agent at one workflow. Review the change request it opens, then add agents and connectors as trust grows. Both projects ship open source, so the move is additive rather than a rebuild.
