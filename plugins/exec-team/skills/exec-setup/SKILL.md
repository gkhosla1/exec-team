---
name: exec-setup
description: >
  This skill should be used when the user wants to set up, add or change an executive team for a project:
  "set up my exec team", "add the exec team to this project", "/exec-setup", "add a role to my team",
  "change when my brief runs", or when another exec-team skill finds no team config. Interviews the user,
  writes the project's team config and working docs, and schedules the brief.
metadata:
  version: "0.2.0"
---

# Set up an executive team for a project

Goal: a team config and four working docs for this project, and (if wanted) a scheduled brief. Keep the interview short: about 6 questions in two rounds of multiple choice (AskUserQuestion takes at most 4 at a time), and pre-fill anything already known from the conversation, the attached Project's docs or the working folder.

## 1. Find where the team will live
- **Attached claude.ai Project** (preferred: shared across chats, devices and scheduled runs): docs go under `claude/exec/` with the Projects tool.
- **Check it's the right Project first.** Read the Project's name and description (`project_info`). If the Project is not obviously the one the team is for (for example, it's a framework, template or unrelated project), ask before writing anything. Never write a project's team into another project's Project.
- **No Project:** use an `exec/` folder in the working directory and say so. A local folder is not visible to scheduled runs (each run starts in a fresh session), so with local storage offer no scheduled brief; tell the user that attaching a Project enables one.
- If a config already exists, this is an edit: read it, ask only what's changing, and write it back.

## 2. Learn the project (read before asking)
Read the Project's existing docs (spec, notes) and the conversation. Draft the company brief yourself: what it is, stage, how it makes money (or plans to), stack and running costs, current priorities in order, the owner's working preferences. Ask the user only to confirm or correct the draft.

## 3. Interview (ask only what isn't already known)
Round 1:
1. **Roster.** Offer the default six from `references/roles.md` (Chief of Staff always included), plus any optional roles that fit this project. Allow renaming, merging (e.g. Product + Customer Experience before launch) and adding a custom role.
2. **Customer panel.** Propose 3–5 personas specific to the project's audience; let the user adjust.
3. **Brief schedule.** Days, time, time zone. Suggest twice a week (e.g. Mon and Thu late afternoon) or weekly; "no scheduled brief" is fine.

Round 2:
4. **Delivery.** Email (to which address, via the connected ~~email tool), a message in a ~~chat channel (e.g. Slack) if connected, or a notification only (the run's result plus a push notification, for people without an email connector).
5. **Sources.** Which ~~email label/folder the team may read (create it if the email connector can; the user adds a filter that routes relevant mail there); any digest email the project already sends or will send; partner and service senders to watch; topics for light web checks; other connectors. Explain the privacy rule: the team reads only that label.
6. **Alerts.** What should jump to the top of a brief (suggest 3–4 based on the project). **Each alert must be checkable from the sources.** "Partner email unanswered 3 days" can't be judged if sent mail isn't in the label; rephrase it (e.g. "partner email in the label older than 3 days with the matching action item still open") or drop it.

## 4. Write the docs
Using the Projects tool (`project_write`) or local files:
- `team-config.md` from `references/config-template.md`, with each chosen role's full card copied in and a **Watches** checklist written for this project's actual sources.
- `company-brief.md`: the confirmed draft from step 2.
- `decisions-log.md`: table (Date | Decision | Why | Dissent | Revisit), seeded with decisions already evident from the Project's docs or conversation, and "Set up executive team" as the first entry. **Revisit** is a date or a trigger ("at 1,000 members") for the retro; leave blank if none.
- `action-items.md`: Open table (Added | Item | Owner | Due) seeded with known open items, and a Done table (Done | Item | Owner).
- `brief-log.md`: the briefing's memory between runs. Start it with "No briefs yet." (Format is in `references/config-template.md`.)

## 5. Schedule the brief (if wanted, and only with a Project)
Use the session's scheduling tool for recurring tasks (search for it with ToolSearch if needed; never use session-local cron tools, which disappear when the session ends). Set the user's time zone. Name it "<Project> exec brief". The prompt must stand alone: each run starts fresh, may not have this plugin installed, and must find the Project by name:

> Run the exec-briefing skill for the <Project> executive team. The team config is at `claude/exec/team-config.md` in the claude.ai Project "<Project name>". If the skill isn't available, read the config and follow its Brief, Sources and Alerts sections: gather only from the listed sources (email: only the label "<label>", only since the last run recorded in `claude/exec/brief-log.md`), write a brief under ~200 words with at most 3 owned action items and urgent items first, deliver it as the config says (<delivery>), update `action-items.md` and `brief-log.md`, and end with one line confirming delivery. Never invent numbers; a missing source is a finding.

Tell the user in one sentence when it will first run and whether runs ask for approval. Offer to run the first brief now so they can see it.

## 6. Finish
Summarize in a few lines: roster, panel, schedule, sources, and what the user still has to do (e.g. create the email filter, forward an inbox, set up a digest). Mention they can now say "ask the team about …", "ask <role> …", "quick meeting on …", or "run a retro".
