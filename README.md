# mywant-teams-webhook-plugin

A [MyWant](https://github.com/onelittlenightmusic/MyWant) plugin that adds the **Teams Notify** want type.

Receives messages from Microsoft Teams Outgoing Webhooks via HTTP POST and exposes them to downstream wants.

## Requirements

- [MyWant](https://github.com/onelittlenightmusic/MyWant) installed and running
- Microsoft Teams with Outgoing Webhook configured

## Installation

```sh
git clone https://github.com/onelittlenightmusic/mywant-teams-webhook-plugin \
  ~/.mywant/custom-types/mywant-teams-webhook-plugin
```

Then restart MyWant (`./bin/mywant stop && ./bin/mywant start -D`).

## Usage

```yaml
metadata:
  name: teams-inbox
  type: teams_notify
spec:
  params:
    webhook_secret: ""   # optional: base64-encoded HMAC secret from Teams
    channel_filter: ""   # optional: Teams channel ID to filter
```

The webhook endpoint is available at:
```
POST /api/v1/webhooks/{want-name}
```

Configure this URL in your Teams Outgoing Webhook settings.

## Test with curl

```sh
curl -X POST http://localhost:8080/api/v1/webhooks/teams-inbox \
  -H "Content-Type: application/json" \
  -d '{"type":"message","text":"hello","from":{"name":"Test User"},"channelId":"msteams"}'
```
