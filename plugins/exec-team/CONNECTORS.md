# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool you connect in that category. The plugin describes workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category | Placeholder | Options | Used for |
|---|---|---|---|
| Email | `~~email` | Gmail, Microsoft Outlook | Reading one approved label/folder (digests, partner mail, feedback) and sending the brief to the owner |
| Chat | `~~chat` | Slack, Microsoft Teams | Optional: posting the brief to one configured channel instead of emailing it |

Without either, briefs can be delivered as a notification (the scheduled run's result plus a push notification), and consulting needs no connector at all.

Optional: any read-only connector you list in your team config (analytics, project tracker, docs) can be added as a source.
