# actions-notify-slack/raw

Sends a free-text message to a Slack incoming webhook. Use it for notifications that are not deployments; for deployments, use the [main action](../README.md).

The message shows the `details` text, followed by a line with a link to the workflow run, the branch/tag and who started it. It has a coloured sidebar:

| Status      | Colour |
|-------------|--------|
| `success`   | Green  |
| `cancelled` | Yellow |
| anything else (e.g. `failure`) | Red |

## Inputs

| Name          | Required | Default      | Description |
|---------------|----------|--------------|-------------|
| `webhook-url` | yes      |              | Slack incoming webhook URL (use a secret) |
| `details`     | yes      |              | Message text (Slack mrkdwn) |
| `status`      | no       | `job.status` | `success`, `failure` or `cancelled`, sets the sidebar colour |

## Usage

```yaml
- name: Notify Slack
  if: always()
  uses: DirektoratetForByggKvalitet/actions-notify-slack/raw@main
  with:
    webhook-url: ${{ secrets.ARKITEKTUM_SLACK_CICD_WEBHOOK_URL }}
    details: "Nightly import of *${{ github.event.repository.name }}* finished"
```

The `ARKITEKTUM_SLACK_CICD_WEBHOOK_URL` webhook url is added as an organization secret in the DiBK Github organization, and is available in all repositories.

`details` uses Slack mrkdwn: `*bold*`, `_italic_`, `` `code` ``, `<https://example.com|link text>`. Use a YAML block scalar (`details: |`) for multi-line messages.

Use `if: always()` so the notification is also sent when earlier steps fail.
