# actions-notify-slack

Sends a deployment notification to a Slack incoming webhook. The message has a coloured sidebar:

| Status      | Colour |
|-------------|--------|
| `success`   | Green  |
| `cancelled` | Yellow |
| anything else (e.g. `failure`) | Red |

## Inputs

| Name          | Required | Default                 | Description |
|---------------|----------|-------------------------|-------------|
| `webhook-url` | yes      |                         | Slack incoming webhook URL (use a secret) |
| `app-name`    | no       | repository name         | Application name |
| `version`     | no       |                         | Deployed version |
| `status`      | no       | `job.status`            | `success`, `failure` or `cancelled` |
| `details`     | no       |                         | Extra text (Slack mrkdwn) |

## Usage

```yaml
- name: Notify Slack
  if: always()
  uses: DirektoratetForByggKvalitet/actions-notify-slack@main
  with:
    webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
    version: ${{ github.sha }}
    details: Deployed to *production*
```

Use `if: always()` so the notification is also sent when earlier steps fail.
