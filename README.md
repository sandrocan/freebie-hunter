# OpenClaw Freebie Hunter Plugin

OpenClaw Freebie Hunter is a publishable plugin bundle for finding free
Kleinanzeigen listings, scoring them conservatively for resale potential, and
preparing human-approved outreach.

The bundle contains no runtime code and no secrets. It ships reusable skills,
data-contract templates, and cron-job examples that users can copy into their
own OpenClaw workspace.

## What Is Included

| Path | Purpose |
|---|---|
| `.codex-plugin/plugin.json` | Bundle manifest for OpenClaw/Codex-compatible plugin installs |
| `skills/freebie-hunter/SKILL.md` | Main workflow for collector, review, queue, report, and outreach behavior |
| `skills/freebie-evaluator/SKILL.md` | Conservative valuation scorecard for free classified listings |
| `templates/state/freebie-hunter/` | Empty state files and the shared data contract |
| `templates/cron/jobs.example.json` | Optional scheduled task examples |

## Install Locally

From this repository root:

```bash
openclaw plugins install .
openclaw plugins enable openclaw-freebie-hunter
openclaw gateway restart
```

Then start a new OpenClaw session and ask it to use the Freebie Hunter workflow.

## Workspace Setup

Copy the templates into the workspace that should own the data:

```bash
mkdir -p state/freebie-hunter reports
cp templates/state/freebie-hunter/*.json state/freebie-hunter/
cp templates/state/freebie-hunter/contract.md state/freebie-hunter/
```

The first run is intentionally safe. If `config.json` is not configured, the
collector must ask for a city or a copied Kleinanzeigen "Zu verschenken" search
URL before fetching anything.

## Optional Cron Jobs

`templates/cron/jobs.example.json` is a sanitized starter file. Before importing
it, adjust:

- agent IDs to match your OpenClaw setup
- schedules and timezone
- delivery channel or disable delivery

No Telegram, Discord, API, gateway, or personal tokens are included.

## Publishing Notes

This branch is reduced to the plugin bundle only. It should be safe to publish
to a GitHub repository or package archive for ClawHub after you fill in the
publisher URLs in `.codex-plugin/plugin.json`.
