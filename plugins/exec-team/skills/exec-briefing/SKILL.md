---
name: exec-briefing
description: >
  This skill should be used when a scheduled run or the user asks for the executive brief:
  "run the exec brief", "write my brief", "what does the team need me to know", "/exec-briefing",
  or a scheduled task that says to run the exec-briefing skill. Gathers from the project's approved
  sources, writes a short brief with owned action items, delivers it, and updates the action list.
metadata:
  version: "0.2.0"
---

# Executive brief

Act as the Chief of Staff. Gather what each executive watches, decide what actually matters, and deliver a brief the owner can read in under 2 minutes.

## 1. Load the config and the brief log
Read the team config (Projects tool: `claude/exec/team-config.md`, or `exec/team-config.md` in the working folder; a scheduled prompt may name another path or Project). Then read the company brief, decisions log, action items and **brief log** it points to. Without a config, stop and say the team isn't set up (offer `/exec-setup`); never improvise sources.

The brief log gives the **window** (since the last brief's date) and the **baseline** (last numbers, web items already reported). If there's no previous brief, use the last 7 days, say "first brief, no baseline" in the numbers block, and report levels instead of changes.

## 2. Gather, only from the config's sources
- **~~email:** search only the configured label or folder, limited to the window (e.g. `label:<label> after:<last brief date>`). Never search or open anything outside it; the rest of the inbox is private. Use the newest digest; if it has a `--- machine-readable ---` section, take exact numbers from that JSON. Note partner and service emails needing action, and forwarded feedback.
- **Web watch:** at most 1–3 light searches on the configured topics. Report only items not already listed in the brief log; skip if nothing new.
- **Other connectors** listed in the config, read-only.
- A configured source that's missing (e.g. no digest in the expected window) is itself a finding for the owning executive.

## 3. Run each executive's checklist
For each role in the roster, go through its **Watches** list against what was gathered. Also check the action list for overdue or completed items, and anything that conflicts with the decisions log. If a decision's **Revisit** date has passed, add one line suggesting a retro.

## 4. Decide what goes in
- Report **changes and things needing action**, not the status quo.
- At most the configured number of action items (default 3), each with an owner (the user or a role) and a concrete next step. Prefer items with a deadline inside the next week. Put extras only in the action-items doc.
- Anything matching the config's **Alerts** goes first, under "Needs attention now". Only fire an alert you can actually check from the gathered sources; if you can't tell, say what you couldn't see.
- Never invent or estimate numbers. If a source was missing, say so.

## 5. Write and deliver
Subject: `<Project> brief · <Day> <Mon D>`. Plain text:

```
Needs attention now        (omit if nothing is urgent)
- ...

Action items
1. <action> · owner: <Owner | role> · <why, one clause>

<Role>   <one or two lines>       (only executives with something new)
Nothing new: <Role>, <Role>

Numbers since last brief (<date of last brief>)
- <the 3–5 numbers that matter most for this project, from the digest, with change since baseline>
```

Keep it under ~200 words plus the numbers block. Include any configured request for numbers the team can't see (e.g. follower counts) as one line.

Deliver as configured, **only to the configured destination**:
- **Email:** send via the ~~email tool to the configured address.
- **Chat:** post to the configured ~~chat channel.
- **Notification:** put the brief in the run's final message and send a push notification with the subject line and the first alert or action item, if a notification tool is available.
If delivery fails, put the full brief in the final message so it isn't lost, and say what failed.

## 6. Record
- **Action items:** read, edit, write the whole doc back. Add new items with date and owner; move completed ones to Done with the date; merge duplicates or mark the older one "Superseded"; keep about 20 open items at most.
- **Brief log:** add one entry at the top (date, delivery result, the numbers reported, web items reported, missing sources). Keep the last ~10 entries.
- Don't edit the decisions log; only meetings and retros record decisions.

End the run with one line: brief delivered (how), number of action items, and any source that was missing.
