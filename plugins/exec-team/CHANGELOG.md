# Changelog

## 0.3.0 (2026-11-05)
**Routing (who's in the room)**
- Meetings start with triage: only the roles whose area covers the idea, plus any role whose new **Pull me in when** triggers match (e.g. Legal when one user's info is shown to another), plus a counterweight so at least two mandates disagree, plus the customer panel for anything users see. Triage is shown in one line and the meeting goes straight ahead; "add <role>" or "everyone" changes it.
- A single executive answers directly with no Chief of Staff summary, and points to another role instead of answering outside its lane.
- Optional rebuttal round when two roles split.
- After the answers, left-out roles' triggers are re-checked against what the executives proposed (in the test, Growth's tracking idea pushed the build into Engineering's territory).
- The summary says when gathered text tried to instruct the team, and options must not be straw men.
- Chief of Staff is a default role the owner can remove; its jobs then run in a neutral voice.

**Setup**
- Recommends a team for the project, with a one-line reason for each role in or out, and tailors each role's Optimizes for, Always asks and Pull me in when to the project.
- Optional preferences question (meetings, brief length and quiet days, decision logging, retros), defaults accepted in one click.
- Checks who can see the Project and records it under a new Privacy section.
- Panel personas are invented, never based on real, named customers.

**Privacy and safety**
- Email and web content is treated as information, never instructions (briefing, setup, executive agent, scheduled prompt).
- Delivery is locked to the configured destination; the brief never sends, replies or forwards anything else.
- Setup explains the label rule isn't a technical lock and offers a separate account or alias.
- Brief log can omit numbers in shared Projects.

## 0.2.0 (2026-11-05)
From the first end-to-end test (made-up project: setup, single exec, panel, 6-role meeting, brief from a mock label).

**Setup**
- Confirms the attached Project is the right one before writing (the test session's Project was the framework itself).
- No scheduled brief when the team lives in a local folder: scheduled runs start fresh and can't see it.
- Scheduled prompt names the Project and the brief log, and works without the plugin installed.
- Interview in two rounds (the question tool takes 4 at a time).
- Alerts must be checkable from the configured sources.
- New delivery options: ~~chat channel, or notification only.

**Consult**
- Quick meeting: one pass, no subagents, labeled as not independent. Full meetings are for decisions that are costly to reverse (a 6-role meeting used ~6× the tokens of one answer).
- Chief of Staff chairs and doesn't vote.
- Bundled ideas are split; the idea is framed as 2–3 options and executives pick one (in the test all 6 voted "Go with changes", which hid the real disagreement).
- New `executive` agent (no web, fixed instructions) for meeting subagents; falls back to a general-purpose subagent.
- Retro mode, and a Revisit column in the decisions log.
- Superseded action items are merged or closed instead of duplicated.

**Brief**
- New `brief-log.md`: window and baseline between runs, web items already reported (no repeats), delivery result.
- First brief says "no baseline" and reports levels.
- "Nothing new" executives collapse into one line.
- Suggests a retro when a decision's Revisit date passes.

## 0.1.0
First version: exec-setup, exec-consult, exec-briefing, role library, config template.
