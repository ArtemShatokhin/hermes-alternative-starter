# Getting started with the open-source Kortix starter

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own. This starter takes that from a description to a running session in three commands, then explains the one agent and one skill it ships.

## Three commands to a running session

```bash
# 1 · Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2 · Clone this starter and make it your project
git clone https://github.com/ArtemShatokhin/hermes-alternative-starter my-company
cd my-company

# 3 · Ship the project, then start a session
kortix ship
kortix sessions new --prompt "Write this week's digest and open a change request."
```

`kortix ship` pushes the repo and brings the project live. `kortix sessions new` starts a session, which boots its own cloud computer on a branch named after the session. The agent can install, run and break anything there; only what it commits survives.

From the same terminal, `kortix chat` talks to the session's agent, and `kortix cr ls` lists the change requests it opens. Session work reaches `main` through a change request, and merge is default-deny for agents.

## The manifest

`kortix.yaml` is the file the platform treats as authoritative for a project. This starter is a v2 manifest with one agent and one trigger:

```yaml
kortix_version: 2
default_agent: starter

project:
  name: my-company
  description: What this project is.

agents:
  starter:
    file: agents/starter.md
    connectors: all
    skills: all
    secrets: all
    kortix_permissions: all

triggers:
  - slug: weekly-digest
    name: Weekly digest
    type: cron
    agent: starter
    enabled: true
    cron: 0 9 * * 1
    timezone: UTC
    prompt: |-
      Read the last week of commits and change requests in this project,
      write the digest in the team's format, and open a change request with it.
```

The `agents:` block sets governance only: which connectors, secrets and permissions the agent may reach. The behavior lives in the agent file, which the next section covers. A trigger starts a session on a cron schedule or a signed webhook with nobody present, and the `cron` line here fires every Monday at 09:00 UTC for the `starter` agent.

## The example agent

`agents/starter.md` is the behavior half of the agent. It is a plain markdown file the harness reads in the sandbox and in your editor.

```markdown
---
description: The starter agent for this project.
mode: primary
---

You are the starter agent for this Kortix project. Kortix is open source, so everything you do here is a file the team can read and review.

Follow the team's skills when one matches the job. Read skills/weekly-digest/SKILL.md before you write a digest.

Working rules:
- Do the work on your own cloud computer. Commit what is finished; nothing else survives.
- When the work is ready, open a change request against main and describe what changed.
- Ask for approval before an action that sends, pays or deletes.
```

An agent is `agents/<name>.md` for behavior plus an `agents.<name>` block in `kortix.yaml` for governance. The manifest never holds the prompt or the model; the `.md` does. That split lets you version an agent's behavior and its permissions in the same reviewable diff.

## The example skill

`skills/weekly-digest/SKILL.md` is the skill the agent reads when the job is a digest. A skill is markdown that encodes how the company does one job.

```markdown
---
name: weekly-digest
description: Write the weekly digest from the week's commits and change requests.
---

# Weekly digest

Kortix is open source, so this skill is a file the team can edit and review like any other.

## Steps
1. Read the commits on main and the change requests opened in the last seven days.
2. Group the work by team. Leave out anything that did not land.
3. Write the digest: one line on what shipped, one line per team, one line on what is blocked and who owns it.
4. Open a change request with the digest at reports/weekly-digest.md.
```

Skills load from `skills/<name>/SKILL.md`, and the manifest's `skills: all` gives the agent access to every skill in the repo.

## Where to go next

[Kortix vs Hermes Agent](kortix-vs-hermes.md) compares the platform with the personal agent it replaces, and [Self-hosting](self-hosting.md) runs the stack on your own box. For a migration path from a personal Hermes setup, see [migrate from Hermes](https://hermesalternative.com/migrate-from-hermes).
