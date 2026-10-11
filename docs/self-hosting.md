# Self-hosting the open-source Kortix starter

Kortix is the open-source AI Operating System, and this starter runs on your own infrastructure as one Docker Compose stack. Self-hosting gives a team the whole platform on a box it controls: the control plane, the git repo that holds the agents and skills, and the review path for what the agents change.

## What you own

Everything you configured stays in one git repo you own: the agents, the skills, the memory, the connector config, and the triggers. The Kortix stack adds the control plane that runs them. That stack is the frontend, the API, the LLM gateway, and the Supabase distribution in a single Docker Compose file.

Agent sessions run on a separate sandbox provider, not on this stack. The default provider is Daytona; Platinum and E2B are also supported. Keeping the control plane and the work apart means a busy session does not starve the instance that runs it.

## The steps

```bash
# 1 · Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2 · Point DNS, then initialize the instance
kortix self-host init --domain kortix.example.com

# 3 · Start the stack and set your provider key
kortix self-host start
kortix self-host configure
```

Open ports 80 and 443 for the bundled Caddy proxy, which issues the TLS certificate, and point an A/AAAA record for your domain and for `api.<domain>` at the box. `configure` prompts once for the sandbox provider key and, optionally, a managed-git token. Keep the default 640 MiB memory limit on an 8 GiB host; raise it to 1 GiB when API traffic reaches the limit on a 16 GiB host.

To try the stack with no domain, start it behind a Cloudflare tunnel instead with `kortix self-host init --tunnel cloudflare`. The tunnel URL changes on every restart, so keep a tunnel instance for evaluation.

## What self-hosting changes

Self-host is free. You pay your own model and compute bills. The first run asks six things and no model key, GitHub connects in the dashboard under Settings → Git, and models are BYOK in the app. A self-hosted instance uses your own key by default, which lets a team hold one key it can rotate for every member's agent.

The instance stays reachable so the sandbox can call back, and `kortix self-host start` pulls its images from docker.io. Plan for a host with a public domain, since the sandbox reaches it from outside.

Updates run automatically. Pin an exact version with `kortix self-host update --tag <version>`, or turn the updater off with `--auto-update off`. There is no separate backup system: each instance keeps its database in `volumes/db/data` and its files in `volumes/storage`, both under `~/.config/kortix/self-host/<instance>/`, and its `.env` holds every secret and signing key. Back up all three before a destructive command.

## What a team adds on top

Self-hosting the platform does not change how the work is governed. Per-resource permissions for people and agents, roles, groups, and an audit trail come with it. Approval gates you set, off until you set them. Session work reaches main through a change request, and merge is default-deny for agents. Secrets are encrypted at rest with a key per project. One isolated sandbox per session keeps each task on its own machine and branch.

For how this compares with running a personal agent on your own box, see [self-hosting a Hermes alternative](https://hermesalternative.com/self-hosting-hermes-alternative). To run the starter without self-hosting, [Getting started](getting-started.md) covers the cloud path.
