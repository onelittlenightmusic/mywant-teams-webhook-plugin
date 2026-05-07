---
name: mywant-teams-webhook-plugin
description: Microsoft TeamsのOutgoing WebhookメッセージをMyWant want typeとして受信するプラグイン。TeamsからのHTTP POSTメッセージを受信・バッファリングし、下流のwantに転送する。
compatibility:
  requires:
    - MyWant server running
    - Microsoft Teams with Outgoing Webhook configured
metadata:
  output-format: agent-based
  note: This plugin requires the teams_notify Go implementation in the main binary. YAML-only installation requires the binary to include teams_webhook_types.go and agent_monitor_teams_webhook.go.
---

## 使い方

MyWant want typeとして使用する:

```yaml
metadata:
  name: teams-inbox
  type: teams_notify
spec:
  params:
    webhook_secret: ""
    channel_filter: ""
```

WebhookエンドポイントURL:
```
POST /api/v1/webhooks/{want-name}
```

## 状態フィールド

- `teams_latest_message` — 最新受信メッセージ
- `teams_messages` — 直近20件のFIFOバッファ
- `teams_message_count` — 受信件数
- `webhook_url` — このwantのwebhookエンドポイントパス
