# OpenClaw alternative, self-hosted: Kortix, the open-source CompanyOS

Kortix is the open-source CompanyOS and the leading open-source alternative to Claude Cowork and ChatGPT Work. This repository is the self-hosted route to it for teams that run OpenClaw and now need company-scale agent work: your agents, their skills, your company memory, and every connector in one git repo you own, each session on its own isolated machine, and every change read and approved by a person before it lands.

If you are still choosing, start at [openclaw-alternative.com](https://openclaw-alternative.com/), the companion site that maps this ground page by page.

## Why teams look past OpenClaw

OpenClaw is a capable personal assistant. Its own repository calls it an open-source AI assistant that runs on your own computer and meets you in the channels you already use, and its documentation describes one Gateway process that serves a laptop or a shared team deployment, with configuration the only difference between the two ([OpenClaw's repository](https://github.com/openclaw/openclaw), [OpenClaw's docs](https://docs.openclaw.ai/)). That design fits one person, or a small group that wants the same assistant on hardware they own.

Company work asks for two things an assistant does not carry: a configuration a team can review together, and a step where a person approves what takes effect. Kortix keeps the agents, skills, memory, and connectors in one git repo, and it lands session work through a change request a person reads as a diff.

## The two decisions that separate them

Where the configuration lives decides how much of the operation a team can inspect and roll back. Who reviews the finished work decides what a team can safely hand over. The table sets the two projects against each other on those decisions.

| | Kortix | OpenClaw |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | Yes. MIT-licensed. |
| Where configuration lives | Files in one git repo you own. | A file on the machine that runs the Gateway. |
| Who reviews work | A person reads the change request and merges it. | The assistant acts and replies in your chat. |
| Session isolation | One isolated sandbox per session. | Tools run on the host unless you configure sandboxing. |
| Models | Any model, your keys. | Hosted and local models, swappable harness plugins. |
| Where it runs | Kortix Cloud, your VPC, or your own on-prem network. | Your own computer or server. |

The OpenClaw rows describe what OpenClaw publishes on its own repository and docs site, checked October 2026.

## Self-host Kortix in four commands

Self-host is free, and you keep your own model keys. Kortix runs as one Docker Compose stack, and agent sessions run on a separate sandbox provider.

```sh
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host configure
```

The full walk-through, with the DNS records, the status and log commands, updates, and backups, is in [self-host an OpenClaw alternative](docs/self-host-openclaw-alternative.md).

## Guides in this repository

- [What is OpenClaw?](docs/what-is-openclaw.md): a sourced primer from OpenClaw's own repository and docs, and where its design stops for company work.
- [Kortix vs OpenClaw](docs/kortix-vs-openclaw.md): the head-to-head, built row by row from OpenClaw's own live materials.
- [Self-host an OpenClaw alternative](docs/self-host-openclaw-alternative.md): the prerequisites, the commands, the boundary, and the backups.
- [FAQ](docs/faq.md): the questions teams ask before they move company work onto Kortix.

## Where to read more

The companion site covers each question in depth:

- [The OpenClaw alternative for company agent work](https://openclaw-alternative.com/)
- [Kortix vs OpenClaw](https://openclaw-alternative.com/kortix-vs-openclaw)
- [Open source OpenClaw alternatives](https://openclaw-alternative.com/openclaw-alternatives)
- [Self-host an OpenClaw alternative](https://openclaw-alternative.com/self-host-openclaw-alternative)
- [What is OpenClaw](https://openclaw-alternative.com/what-is-openclaw)
- [Migrate from OpenClaw](https://openclaw-alternative.com/migrate-from-openclaw)

Kortix is open source. The code lives at [Kortix on GitHub](https://github.com/kortix-ai/suna).

[Try Kortix](https://kortix.com) for the managed cloud, or [read the docs](https://kortix.com/docs).


Newer pages on the same site answer the adjacent questions: [OpenClaw vs Hermes](https://openclaw-alternative.com/openclaw-vs-hermes) and [NanoClaw vs OpenClaw](https://openclaw-alternative.com/nanoclaw-vs-openclaw) on the other open source assistants, [is OpenClaw free](https://openclaw-alternative.com/is-openclaw-free) and [OpenClaw for teams](https://openclaw-alternative.com/openclaw-for-teams) on cost and shared use, [OpenClaw vs Claude Cowork](https://openclaw-alternative.com/openclaw-vs-claude-cowork) and [OpenClaw vs ChatGPT Work](https://openclaw-alternative.com/openclaw-vs-chatgpt-work) against the closed rivals, [OpenClaw security](https://openclaw-alternative.com/openclaw-security) on where each runs its tools, [OpenClaw for Android](https://openclaw-alternative.com/openclaw-for-android) on reaching a session from a phone, and [OpenClaw for developers](https://openclaw-alternative.com/openclaw-for-developers) on the API and harness.

Before you switch anything, [the OpenClaw setup guide](https://openclaw-alternative.com/openclaw-setup-guide) walks the install, onboarding and Gateway verification steps and then the point where one gateway stops serving a team.
