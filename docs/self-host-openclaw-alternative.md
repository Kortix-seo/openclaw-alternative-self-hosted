# Self-host an OpenClaw alternative: run the open-source Kortix AI Operating System end to end

Self-hosting Kortix keeps the whole control plane for company agent work inside your own network: accounts, projects, repos, secrets, connectors, policy, and audit. Kortix is the open-source AI Operating System, and self-host is free. This guide covers what to have ready, the commands that take a Linux box to a running instance, what runs on the box and what does not, and how updates and backups work. The steps follow the [Kortix self-hosting docs](https://kortix.com/docs/host), checked October 2026.

## What to have ready

- A Linux box. The CLI runs on macOS and Linux, and on Windows through WSL.
- A domain, with A or AAAA records for the domain and for `api.<domain>`, both pointing at the box.
- Ports 80 and 443 reachable, so the bundled Caddy proxy can issue a TLS certificate.
- A model provider key, added later in the model picker.

## Install and start

```sh
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host configure
```

The installer downloads a prebuilt binary for macOS or Linux; run `kortix version` to confirm it is on your path. `kortix self-host init` writes the instance under `~/.config/kortix/self-host/<instance>/`. The first run asks six things and no model key: Pipedream is optional, and your model key is added later in the app. `kortix self-host start` brings up the stack. `kortix self-host configure` sets the sandbox provider key and an optional managed-git token.

While the stack comes up, `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor` report what is happening.

To evaluate with no domain, use a Cloudflare tunnel instead: `kortix self-host init --tunnel cloudflare`, then `kortix self-host start`. The tunnel URL changes on every restart, so use this mode for evaluation and not for production.

## After the stack starts

Open your domain in a browser and sign up with the admin email. Two settings make the instance usable: connect GitHub at Settings, then Git, and connect your own model key in the model picker. Create a project in the dashboard, point the CLI at your instance, and link a repo that holds `agents/`, `skills/`, `memory/`, and `kortix.yaml`:

```sh
kortix projects ls
kortix projects link <project-id>
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls
```

The session works on its own sandbox and its own branch. Its work reaches the default branch only when you read the change request and merge it.

## What runs on the box, and what does not

| On the box | Off the box |
| --- | --- |
| The frontend, the API, the LLM gateway, and the bundled Supabase distribution. | Agent sessions, on a separate sandbox provider. |
| Accounts, projects, repos, secrets, connectors, policy, and audit. | Platinum is the default provider; Daytona remains available as a legacy fallback. |
| One Docker Compose stack. | The box stays reachable so a sandbox can call the API. |

The boundary matters for capacity planning and for a security review. A self-hosted instance has no managed model lineup, so every model call routes through the LLM gateway on your own box. For a topology where the sandbox compute also runs inside your network, Kortix scopes that isolated setup with you directly.

## Updates and backups

Each instance updates itself automatically. Pin an exact version with `kortix self-host update --tag <version>`, or turn the updater off with `--auto-update off`.

Kortix has no separate backup system. Each instance stores its data as two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` for the Postgres database and `volumes/storage` for file storage. The instance `.env` file holds every secret and signing key it uses. Back up all three before you run a destructive command.

## How this differs from self-hosting OpenClaw

OpenClaw self-hosts as one Gateway process on your own machine, with configuration in `~/.openclaw/openclaw.json` and tools running on the host for the main session unless you configure sandboxing ([OpenClaw's repository](https://github.com/openclaw/openclaw)). Kortix self-hosts as a Docker Compose stack that runs a company repo, with each session on its own isolated machine off the box and every change landing through review.

For the wider field of self-hosted options, see the [self-host guide](https://openclaw-alternative.com/self-host-openclaw-alternative) on the companion site.

Kortix is open source. The code lives at [Kortix on GitHub](https://github.com/kortix-ai/suna).

[Try Kortix](https://kortix.com) for the managed cloud.
