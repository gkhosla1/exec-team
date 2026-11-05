# Changelog

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
