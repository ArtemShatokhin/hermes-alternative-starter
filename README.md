# Kortix starter: the open-source Hermes alternative for teams

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. This repository is a copy-and-run starter for a team that has outgrown a personal agent and wants that system running inside its own project.

If you are still weighing the move, [a side-by-side of the open-source Hermes alternatives](https://hermesalternative.com/hermes-alternatives) shows where a personal agent stops and a company platform starts.

## What this starter gives you

A minimal but real Kortix project: one agent, one skill, and one cron trigger, wired the way a production project is wired. Copy the files into your own repo, point the manifest at your tools, and the same layout runs on Kortix Cloud, in your VPC, or on your own on-prem network.

This starter is for a developer or platform lead who already runs an agent and now needs a shared project: more than one person steering it, per-tool rules on what it may touch, and a review path for what it changes.

## What's in the repo

```text
kortix.yaml                       the manifest: the agent, its reach, and a cron trigger
agents/starter.md                 the example agent: behavior, in plain markdown
skills/weekly-digest/SKILL.md     the example skill: how the team writes a digest
docs/getting-started.md           three commands to a running session
docs/kortix-vs-hermes.md          Kortix and Hermes Agent compared, from Hermes' own sources
docs/self-hosting.md              run the whole stack on your own box
```

## Quickstart

```bash
# 1 · Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2 · Clone this starter and open the manifest
git clone https://github.com/ArtemShatokhin/hermes-alternative-starter my-company
cd my-company

# 3 · Bring it live
kortix ship
```

`kortix ship` pushes the repo and brings the project live. Start the first session with `kortix sessions new --prompt "Write this week's digest and open a change request."`, talk to it with `kortix chat`, and review what it proposes with `kortix cr ls`.

## What you take with you

The project is one git repo you own. The agent, the skill, the memory, the connector config, and the trigger are all text, so a change to how the company works arrives as a diff someone reviews.

Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. One isolated sandbox per session, each session on its own isolated machine and branch.

Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free.

## Go deeper

- [Getting started](docs/getting-started.md) walks the three commands and the agent and skill in this repo.
- [Kortix vs Hermes Agent](docs/kortix-vs-hermes.md) compares the two from Hermes' own repository and docs, and gives the decision.
- [Self-hosting](docs/self-hosting.md) runs the stack on your own box, and lists the trade-offs.
- [Kortix on GitHub](https://github.com/kortix-ai/suna) is the platform source.

Kortix is open source. Read it, fork it, audit it.
