# Kortix vs Hermes Agent: the open-source company system and the open-source personal agent

Kortix is open source and built for a whole company. Hermes Agent is open source and built for one operator. Both let you bring your own model and run on hardware you choose. The choice turns on how many people steer the agent, how much you must control what it touches, and whether its history has to survive a review.

Hermes Agent is the self-improving personal agent from Nous Research. Its [repository](https://github.com/NousResearch/hermes-agent) documents a closed learning loop: it creates skills from experience, keeps agent-curated memory, and searches its own past sessions. Its [documentation](https://hermes-agent.nousresearch.com/docs) describes a home on a $5 VPS, a GPU cluster, or serverless infrastructure, seven terminal backends, and 20+ messaging platforms from one gateway.

## Kortix and Hermes Agent, dimension by dimension

| Dimension | Kortix | Hermes Agent |
| --- | --- | --- |
| Open source | Open source. Read it, fork it, audit it. | Yes, open source, with your own model. |
| Designed for | Teams and companies. | One operator. |
| Where the configuration lives | In a git repo you own. | In a config file on the machine you run it on. |
| Per-tool policy | Set each tool to Allow, Ask or Block. | Command approval and DM pairing. |
| Isolation per task | One isolated sandbox per session. | Seven terminal backends, container hardening. |
| Review and history | Work lands through a change request; every action is recorded. | Command approval before a risky call. |
| Where it runs | Kortix Cloud, your VPC, or on-prem. | A $5 VPS, a GPU cluster, or serverless. |
| Model choice | Any model provider with your own keys. | Any model you want, no lock-in. |

Hermes Agent facts are from its own repository and documentation, checked in October 2026; Kortix facts are the platform's own documented capabilities.

## Where Hermes Agent is the right answer

Hermes Agent is a strong personal agent. It runs on a $5 VPS, a GPU cluster, or serverless infrastructure, and it reaches you from the CLI and from Telegram, Discord, Slack, WhatsApp, Signal, and more through one gateway process. Its learning loop creates skills from experience, keeps memory across sessions, and improves the skills it already wrote. One person who wants an always-on agent on a machine they control gets exactly that from Hermes Agent.

## Where Kortix takes over

The questions change the moment more than one person steers the agent, and Kortix answers them inside the product.

- Who may reach which tool? Set each tool to Allow, Ask or Block, down to the arguments of each call. An Ask holds the call until a person approves it, then the agent resumes.
- Where does the work run? One isolated sandbox per session, each session on its own isolated machine and branch.
- What happened, and who signed off? Session work reaches main through a change request, and every action is recorded.
- Who is allowed in? Per-resource permissions for people and agents. Roles, groups, and an audit trail, with SAML 2.0 single sign-on and SCIM 2.0.
- Where does the configuration live? In one git repo the company owns, so an agent's behavior and its permissions move in the same reviewable diff.
- How do secrets stay safe? Secrets are encrypted at rest with a key per project.
- How does it scale? Thousands of agents in parallel on one config, each on its own cloud computer.

## The decision

Choose Hermes Agent when the user is a person: a private agent on a machine they own, in the chat apps they already use, improving its own skills.

Choose Kortix when the user is a team or a company: shared projects with roles, per-tool rules, isolation per session, and a reviewed history, with the configuration in a repo the company owns and can self-host.

A longer version of this comparison is published as [Kortix vs Hermes](https://hermesalternative.com/kortix-vs-hermes). The repo also holds the [self-hosting](self-hosting.md) and [getting-started](getting-started.md) guides.

[Try Kortix](https://kortix.com) to run the team side.
