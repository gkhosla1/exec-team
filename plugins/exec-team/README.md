# Exec Team

A virtual executive team for people building projects with Claude. Each executive has a sharp mandate and argues from it, so you get real disagreement instead of polite agreement. The team can also watch your project and send you a short brief with action items on a schedule.

## What's included

| Skill | What it does | Say |
|---|---|---|
| **exec-setup** | Interviews you about your project, then writes the team config, company brief, decisions log and action list, and schedules your brief | "Set up my exec team" |
| **exec-consult** | Ask one executive, the customer panel, or hold a meeting: full (each executive answers independently) or quick (one pass, cheaper). The Chief of Staff summarizes picks, votes, disagreements and the decision only you can make. Also runs retros on past decisions | "Ask Legal about…", "Ask the team: should we…", "Quick meeting on…", "Run a retro" |
| **exec-briefing** | Gathers from your approved sources, writes a brief under ~200 words with at most 3 owned action items, delivers it (email, chat channel or notification), and updates the action list and brief log | Runs on your schedule, or "run my exec brief" |

## Default roster
Chief of Staff (chair), Product & Design, Growth, Engineering & Data, Business & Partnerships, Legal & Compliance, plus a customer panel of personas. Optional roles (Support, Finance, Operations, Research, Sales) are offered during setup. Every role card is copied into your project's config, so you can edit it per project.

## Where your team lives
In the claude.ai Project attached to your session, under `claude/exec/`:
- `team-config.md`: roster, panel, schedule, sources, alerts
- `company-brief.md`, `decisions-log.md`, `action-items.md`, `brief-log.md`

Without an attached Project, the same files go in an `exec/` folder in your working directory. Scheduled briefs need the Project, because each scheduled run starts in a fresh session.

The plugin also includes an `executive` agent used for independent answers in full meetings.

## Privacy
The team reads only one email label or folder you choose, plus any sources you list in your config. Briefs are sent only to the address in your config.

## Feeding the brief data
Any system can report to the team by emailing a digest into the approved label. Optionally end the email with a line `--- machine-readable ---` followed by JSON, and the brief will use those exact numbers.

## Install
Shared within your organization: install from the org plugin catalog. Outside it:
`/plugin install exec-team --marketplace gkhosla1/exec-team`

## Requirements
- An email connector (see CONNECTORS.md) for monitoring and emailed briefs. A chat connector or notifications work for delivery too. Consulting needs no connector.
- Scheduled briefs need an environment that supports scheduled tasks.

## Version
0.2.0 (see CHANGELOG.md). Built by Griffin Khosla.
