# Skill: daily-summary

> Triggered at end of day. Synthesizes vault meeting files and session logs
> into a daily note, surfaces friction and proposed fixes, and updates
> the session handover.

Trigger phrases: "let's wrap up today", "EOD", "daily summary"

---

## Step 0 — Determine date

Read date from system context. Do not ask. If a specific date is stated
in the trigger (e.g. "daily summary for yesterday"), use that instead.

---

## Step 1 — Read today's sources

Read in parallel:

1. All meeting files matching `meetings/YYYY-MM-DD-*.md` for today's date
2. All session log files in `_meta/session-logs/` dated today
3. `_meta/friction.md` (existing entries, to avoid duplicating)
4. `context/working-principles.md` (existing principles, to avoid duplicating)

List the files found before proceeding.

If no meeting files and no session logs found for today: say so and offer to
stop or synthesize from available context only.

---

## Step 2 — Session signal extraction

Scan all session logs for today and extract:

### A. Friction signals
Every instance where:
* You said "no", "wait", "that's wrong", "not quite", or corrected the output
* Wrong context was applied
* Something had to be re-explained from a prior session
* A capability was missing (no skill, no context file)

For each: capture what happened, root cause, and a proposed fix (specific file
and what to change).

### B. Working principles and logic patterns
Look for moments where your reasoning or instincts were visible:
* A decision you made and why
* A scope call or tradeoff you defended
* How you framed a problem to stakeholders vs. internally
* Any pattern seen 2+ times

For each: draft a candidate principle in plain language. Flag whether it's new
or a repeat of something in `context/working-principles.md`.

### C. Skill gaps
Tasks attempted today where:
* No skill existed and one should
* A skill existed but needed repeated correction

---

## Step 3 — Generate daily note

Output path: `daily/YYYY-MM-DD.md`

### Note structure

```
---
date: YYYY-MM-DD
meetings: [list of meeting files read]
tags: [daily]
---

# [Weekday, Month DD YYYY]

## Shape of the Day
2-4 sentences. What kind of day was it: directional, reactive, maintenance,
relationship-building? What was the dominant mode of work?

## What Mattered
3-5 bullets. The things that will still matter in 3 months.
Not a summary of each meeting — synthesize across them.

## Decisions Made
- **[DECISION]** What was decided > "quote if available" — context
If none: No decisions today.

## Open Threads
Unresolved items still in motion. Not action items — things not yet resolved.
- [Thread]: [What's unresolved and why it matters]

## Actions Carried Forward
All open actions from today (from meetings, sessions, and initiative work).

## Energy and Momentum Check
One honest sentence: energy level, where momentum is, anything worth noting.
```

Show the full proposed note. Do NOT write yet.
Ask: "Write this daily note?"

---

## Step 4 — System improvement proposals

Show all of the following. Err toward surfacing more.

### 4A. Friction log entries

```
### YYYY-MM-DD — [Short title]
**What happened:** [what went wrong or was slow]
**Root cause:** [why]
**Improvement vector:** vault structure / skill / CLAUDE.md rule / context file
**Proposed fix:** [specific file and what to change]
```

### 4B. Principle promotion candidates

```
**Candidate principle:** [plain language statement]
**Source:** [what triggered it]
**Status:** NEW or REPEAT
**Proposed action:** Add to principles file / Strengthen existing entry / Watch for more data
```

### 4C. Skill gap entries

```
**Gap:** [task or scenario]
**What happened:** [how it surfaced]
**Proposed fix:** New skill — [name and description] / Update existing skill — [name and what to add]
```

Show all proposals. Do NOT write yet.
Ask: "Apply system improvements?"

---

## Step 5 — Batch initiative updates

Read `context/initiatives/` to identify all relevant initiative files across
all of today's meetings and sessions. One pass, batch all updates together.

For each affected initiative, propose in diff format:

```
### Initiative: [name].md

**Running Narrative** — ADD at top:
> [YYYY-MM-DD] — [2-3 sentence summary]

**Key Decisions** — ADD if applicable:
> | [YYYY-MM-DD] | [Decision] | [Source] |

**Open Action Items** — ADD new or MARK COMPLETE as applicable
```

Show all proposals. Do NOT write yet.
Ask: "Apply initiative updates?"

---

## Step 6 — Write on confirmation

Write each piece only after explicit confirmation:
1. Daily note → after confirming Step 3
2. System improvements → after confirming Step 4
3. Initiative updates → after confirming Step 5

Each gate is independent. Never auto-write anything.

---

## Step 7 — Staging cleanup

Scan `_staging/` for any files (excluding `README.md`).

If files are found, list them:
```
Unconfirmed outputs in _staging/:
- [filename] — [one-line description]
```

For each file, ask: "Save to vault, discard, or keep for next session?"

---

## Step 8 — Update SESSION-HANDOVER.md

After all writes: update the `# RESUME HERE` block to reflect what was written
today and what carries forward to tomorrow.
