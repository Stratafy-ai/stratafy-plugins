# Stratafy Plugins

Claude plugins for Stratafy — the operating system for strategy.

## Plugins

| Plugin | Who It's For | Description |
| --- | --- | --- |
| [`stratafy-guardian`](./stratafy-guardian/) | Strategy guardians, coaches & consultants | Workspace setup, session debriefs, strategy reviews, radar scans |
| [`stratafy-finance`](./stratafy-finance/) | Finance Directors & finance teams | COA design, financial alignment scans, budget mapping, investor prep |
| [`stratafy-team`](./stratafy-team/) | Every team member | Daily/weekly rhythm, strategic context, role-adapted coaching |
| [`stratafy-chief-of-staff`](./stratafy-chief-of-staff/) | Founders, CEOs, Chiefs of Staff | Exec briefs, initiative tracking, alignment checks, decision logs |

## Installation

```bash
claude plugins add Stratafy-ai/stratafy-plugins/stratafy-guardian
claude plugins add Stratafy-ai/stratafy-plugins/stratafy-finance
claude plugins add Stratafy-ai/stratafy-plugins/stratafy-team
claude plugins add Stratafy-ai/stratafy-plugins/stratafy-chief-of-staff
```

## Development

Plugins are developed inside the main Stratafy monorepo and synced here for publishing:

| Local (monorepo)          | Published (this repo)        |
| ------------------------- | ---------------------------- |
| `guardian-plugin/`        | `stratafy-guardian/`         |
| `finance-plugin/`         | `stratafy-finance/`          |
| `team-plugin/`            | `stratafy-team/`             |
| `chief-of-staff-plugin/`  | `stratafy-chief-of-staff/`   |

### Publishing Changes

```bash
# Clone this repo
git clone https://github.com/Stratafy-ai/stratafy-plugins.git /tmp/stratafy-plugins

# Sync whichever plugin changed
rsync -av --delete guardian-plugin/ /tmp/stratafy-plugins/stratafy-guardian/ --exclude='.git'
rsync -av --delete finance-plugin/ /tmp/stratafy-plugins/stratafy-finance/ --exclude='.git'

# Commit and push
cd /tmp/stratafy-plugins
git add .
git commit -m "feat: describe what changed"
git push origin main
```

### Versioning

Each plugin tracks its own version in `.claude-plugin/plugin.json`. Follow semver:

- **Patch** (x.x.1) — fixes to existing commands or skills
- **Minor** (x.1.0) — new skills, new commands, or significant updates
- **Major** (1.0.0) — breaking changes

Bump the version before pushing.

## MCP Connection

All plugins connect to Stratafy via MCP:

```json
{
  "mcpServers": {
    "stratafy": {
      "type": "http",
      "url": "https://app.stratafy.ai/api/mcp"
    }
  }
}
```

## License

Apache-2.0
