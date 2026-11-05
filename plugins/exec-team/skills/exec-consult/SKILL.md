---
name: exec-consult
description: >
  This skill should be used when the user wants input from their executive team on an idea, plan or decision,
  or wants the team to review past decisions: "ask the team", "exec meeting", "quick meeting",
  "what would Growth think", "ask Legal", "run this by the execs", "what does everyone think",
  "ask the customer panel", "run a retro", "how did our decisions turn out", or "/exec-consult".
  Covers one executive, the customer panel, a full or quick meeting, and a retro.
metadata:
  version: "0.2.0"
---

# Consult the executive team

The user is the CEO. Their executives each have a sharp mandate and argue from it; they are not balanced advisors. A meeting where everyone agrees has failed unless the idea is genuinely uncontroversial.

## 1. Load the project's team
1. Find the team config. Look in the attached Project first (Projects tool: `claude/exec/team-config.md`), then in the working folder (`exec/team-config.md`). The config lists the roster with role cards, the customer panel, and where the other docs live.
2. Read the docs the config points to: the company brief, the decisions log (settled calls; never relitigate without new information), and open action items. Skim any project doc relevant to the idea.
3. If there's no config, say in one line that the team isn't set up for this project and offer `/exec-setup`. If the user wants an answer now anyway, use the default roles in `references/roles.md` and what's known from the conversation.

## 2. Pick the format
- **One executive named** ("ask Legal") → answer as that executive, in the conversation, using their role card. No subagents.
- **Customer panel** → each persona reacts in first person, 2–3 lines each.
- **"Quick meeting"**, or a decision that's cheap to reverse (under about a day of work, no money or partner commitment) → a quick meeting (below).
- **"Ask the team" / "meeting" / several roles**, for a decision that's costly to reverse → a full meeting (below), with the named roles or the full roster.
- **"Retro"** → section 5.
- **Unclear** → answer as the 1–2 most relevant executives and offer a meeting in one line.

Before any meeting:
- **Split bundled ideas.** If the idea contains two separable decisions ("offer the pilot *and* build SMS"), say so and meet on the one that matters most, or run them as two numbered questions in the same meeting.
- **Frame the fork.** Turn the idea into 2–3 concrete options (always including the user's own proposal), so executives vote on real alternatives rather than "go with changes" on a vague plan. If the idea is unclear in a way that would change every answer, ask one short question first.

## 3. Hold a meeting
The Chief of Staff chairs and does not vote; every other executive in the roster (or the named ones) answers.

### Full meeting (independent subagents)
Run each executive as a separate subagent in parallel, one per role, so no one anchors on anyone else. Use the plugin's `executive` agent type if it's available, otherwise a general-purpose subagent told not to use tools. Subagents start cold: give each today's date, its role card (copied in full from the config), the idea in the user's words, the options, the relevant parts of the company brief and decisions log, the stage and constraints, and the answer format below. Instruct each to stay strictly in role and to disagree when its mandate says so.

Each subagent carries a fixed start-up cost regardless of answer length, so a six-role meeting costs roughly six times a single answer. That's why quick meetings exist.

### Quick meeting (one pass, no subagents)
Write each executive's answer yourself, in roster order, **before** writing any synthesis, and keep each one strictly to its role card. Label the result "Quick meeting" so the user knows the answers weren't independent. Offer a full meeting if the votes split or the stakes turn out higher than they looked.

### Executive answer format (under ~150 words)
- **Pick:** which option (A / B / C), or "none of these: <alternative>"
- **Vote on the user's proposal:** Go / Go with changes / Not now / No
- **Biggest concern:** one sentence, specific to this idea
- **What I'd change:** 1–3 bullets
- **What would change my vote:** the one fact or result
- **Confidence:** low / medium / high

### Meeting summary (what the user reads)
- **Bottom line:** the recommended call, in one or two sentences.
- **Votes:** picks and votes in one line each, e.g. "Picks: B 4 · A 1 · C 1" and "On your proposal: Go with changes 5 · No 1".
- **Where they disagree:** the real tensions, named by role, 1–3 bullets. This is the most valuable part; never smooth it over. If the votes are unanimous, still name the strongest disagreement within the details, and say plainly whether the unanimity looks real or comes from a hedged option.
- **Your decision:** the specific choice only the user can make, phrased as a question.
- **If you go ahead:** up to 3 action items, each with an owner role.
- Offer to show any executive's full answer.

## 4. Record decisions
Only when the user actually decides: append to the decisions log (date, decision, why, who dissented, and a **Revisit** date or trigger, e.g. "after the pilot ends, July 1") and update action items. Read the doc, edit, and write the whole doc back (Projects tool `project_read` / `project_write`, or the local file). When a new item replaces an existing open one, merge them or move the old one to Done as "Superseded", so the list never holds two versions of the same task. Don't record ideas that were only discussed.

## 5. Retro (how past decisions turned out)
1. From the decisions log, pick entries whose Revisit date or trigger has passed (or the ones the user names; otherwise those older than about 6 weeks, at most 5).
2. For each, gather what's known since: the brief log, action items, and anything the user tells you. Ask the user one short question per decision only where the outcome isn't in the docs.
3. Each relevant executive (usually the one whose mandate it touched plus any dissenter) answers in 2–3 lines: **Outcome** (worked / mixed / didn't / too early), **What we learned**, **Keep, change or reverse**. Dissenters say whether their concern came true. This is a quick-meeting format; use subagents only if the user asks.
4. Chief of Staff summary: one line per decision, then at most 3 action items.
5. With the user's agreement, add an outcome note to the decision's row (e.g. "Retro 2026-07-02: worked; keep") and set a new Revisit if it's still open. A reversal is a new decision row, not an edit of the old one.

## Style
Plain language, short, specific to this project and its stage. Use numbers where available. No generic startup advice and no praise padding.
