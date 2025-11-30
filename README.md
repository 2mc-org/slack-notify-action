# Slack Notify Action

This repository contains a GitHub Action that notifies about workflow results in Slack.

## Inputs

- `results`: Job statuses. Type: `string`. Required.
- `token`: Slack Bot Token. Type: `string`. Optional.
- `runner-token`: Runner Token. Type: `string`. Optional.
- `channel`: Slack Channel where to send the message. Type: `string`. Required.

## Usage

Below is an example of how to use this action in a GitHub Workflow:

```yaml
name: "Notify Slack on Workflow Result"

on: [push]

jobs:
  build: ...
  deploy: ...
  notify:
    runs-on: ubuntu-latest
    needs: [build, deploy]
    if: always()
    steps:
      - name: Slack Notification
        uses: 2mc-org/slack-notify-action@v1
        with:
          results: "${{ join(needs.*.result, ' ') }}"
          token: ${{ secrets.SLACK_BOT_TOKEN }}
          channel: "channel-name"
```
