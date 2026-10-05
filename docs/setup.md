# Self-Hosting and Getting Started with Open-Source Kortix

Kortix is open source, and this guide takes a team from a fresh machine to a running project with reviewed agent work. It covers the install, the project scaffold, the `kortix.yaml` manifest, running a session, reviewing a change request, and self-hosting your own instance.

## Install the CLI

```bash
curl -fsSL https://kortix.com/install | bash
```

The install script downloads the `kortix` CLI. If you prefer zero setup, sign up at [kortix.com](https://kortix.com), create a project in the web app, and start a session with nothing to install locally.

## Scaffold a project

```bash
kortix init
```

`kortix init` creates `kortix.yaml` plus your agents, skills, and runtime config. The project is a git repository, so every change to an agent, a skill, or a connector is a commit you can review.

## The kortix.yaml manifest

Kortix keeps the company configuration in files. Agents and skills are markdown; `kortix.yaml` declares the machine image, the connectors, and the triggers. A minimal manifest looks like this:

```yaml
# kortix.yaml
agents:
  support-triage:
    file: agents/support-triage.md   # what it does, in plain markdown
    connectors: all                  # what it may reach

triggers:
  - slug: daily-digest
    type: cron
    cron: '0 0 9 * * 1-5'
    prompt: Summarize yesterday's support tickets and open a change request with the digest.
```

Set each tool call to allow, ask, or block, down to the arguments of a single call. An ask holds the call until a person approves it, then the agent resumes.

## Run a session

```bash
kortix sessions new --prompt "Reproduce issue #142, fix it, and open a change request"
```

Every session runs in an isolated sandbox on its own branch, on its own cloud computer. The agent can install, run, and break anything, and only what it commits survives. You can start sessions from the web app, Slack, Microsoft Teams, email, mobile, the CLI, or the API, and from cron schedules or signed webhooks with nobody present.

## Review a change request

```bash
kortix cr ls
```

Work reaches the default branch only through a change request that a person approves. Merge is default-deny for agents, so you read the diff before it lands. This is the gate that lets an agent edit its own configuration and still leave an auditable trail.

## Self-host your own instance

Kortix self-hosts for free as one Docker Compose stack: the frontend, the API, the LLM gateway, and a Supabase distribution. Agent sessions run on a separate sandbox provider, with Daytona as the default and Platinum and E2B also supported.

Point an A or AAAA record for your domain and for `api.<domain>` at the box, open ports 80 and 443 for the bundled Caddy proxy, then run:

```bash
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host configure
```

`kortix self-host configure` is an interactive prompt for the sandbox provider key and, optionally, a managed-git token. Check the stack with `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor`.

To evaluate with no domain, use a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use it for evaluation only. Instances update themselves automatically, or pin an exact version with `kortix self-host update --tag <version>`.

## Backups

A self-hosted instance stores its data under `~/.config/kortix/self-host/<instance>/` as `volumes/db/data` (the Postgres database) and `volumes/storage` (file storage). The instance `.env` file holds every secret and signing key. Back up all three before a destructive command. Kortix has no separate backup system.

## Next steps

- Read [Kortix vs OpenWork](vs-openwork.md) for the team-level comparison.
- See the [FAQ](faq.md) for ownership, models, and cost.
- Full command surface: https://kortix.com/docs
