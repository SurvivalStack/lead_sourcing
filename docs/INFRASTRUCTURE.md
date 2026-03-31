# Infrastructure & Automation

## Secrets Management
These secrets are stored in **Repository Settings > Secrets and Variables > Actions**.

| Secret Name | Purpose |
| :--- | :--- |
| `GH_AUTOMATION_TOKEN` | Fine-Grained PAT (2050 expiry) for Project Board GraphQL access. |
| `DISCORD_PROJECT_WEBHOOK` | Base Webhook URL for automated project status alerts. |

## Automation Workflows

### 1. Project Board Sync (`project_updates.yml`)
- **Logic:** GraphQL polling of the **SurvivalStack** organization board.
- **Trigger:** 5-minute cron schedule and `workflow_dispatch` (manual).
- **Outcome:** Syncs board status to issue labels and pings Discord `#github-project`.

### 2. Commit Notifications (Native Webhook)
- **Logic:** GitHub-native webhook for `push` events.
- **Endpoint:** `DISCORD_PROJECT_WEBHOOK` with `/github` suffix.
- **Outcome:** Instant formatted embeds in Discord for every `git push`.

## Discord Integration
- **Channel:** `#github-project`
- **Notification Policy:** Silent by default (white unread dot). Users must opt-in for pings.