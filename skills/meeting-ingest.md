# Skill: meeting-ingest

> Triggered manually after a meeting ends. Fetches and processes a meeting
> transcript into the vault.

Trigger phrases: "ingest this meeting", "process that meeting", "let's file this meeting"

---

## Step 0 — Identify the meeting

Parse the trigger for scope and search signal:

* Named person or title (e.g. "meeting with Sarah", "1:1 with Sarah") → single meeting, search by name/title
* Time signal + "all" (e.g. "all my meetings today") → batch for that date
* Meeting ID provided → fetch directly
* Ambiguous → ask: "Just that one meeting, or all meetings today?"

For each meeting found, show: Title | Date | Inferred type | Participants

If multiple matches, list them and ask which one.

For batch: list all meetings and confirm the full list before processing any.
Then work through them one at a time.

Infer meeting type from title and participant list:

| Type | Signals |
|---|---|
| `standup` | Daily standup, eng team only |
| `sprint` | Planning, retro, demo, refinement |
| `vendor` | External company name in title or participants |
| `cross-team` | PMs or leads from other teams |
| `1:1-manager` | Your manager in participants |
| `1:1-peer` | Peer PM, EM, or designer |
| `external` | Recruiting, interviews, personal, networking |

---

## Step 1 — Load context

Fetch the full transcript.

Check `meetings/_context/` for a matching context file for this recurring meeting.
If one exists, load it before generating the note.

For any participant you don't know, check `people/` for a matching file.

---

## Step 2 — Generate the meeting note

Output path: `meetings/YYYY-MM-DD-[meeting-type].md`

### Note structure

```
---
date: YYYY-MM-DD
type: [meeting-type]
participants: [names]
tags: [meeting-type, relevant initiative tags]
context_loaded:
  - [file] — [trigger reason]
---

# [Meeting Title]
_[Date] | [Duration] | [Participants]_

## Summary
2-3 sentences. What was the meeting for? What was the outcome?

## Discussion Log
Key moments only: decisions, positions, notable exchanges.
Format: `- **[Speaker]:** "exact quote or tight paraphrase"`

## Decisions
`- **[DECISION]** What was decided > "quote if available" — Speaker`

## Action Items
- [ ] [Action] — [Owner] — [Due if stated]

## Open Questions
Unresolved items that need follow-up.
```

**If technical meeting** (standup, vendor, cross-team with engineers), append:

```
## PM Translation Layer

### Plain English Recap
What the technical discussion meant in PM terms: what changed, what was
decided implicitly, what it means for scope, timeline, or risk.
Written for a smart PM who wasn't in the room.

### Injection Points for Next Meeting
Moments where engineers made tradeoffs or scope calls that warrant PM
input. Each as either:
- A question (when the right answer is unclear): "Should we...?"
- A position (when direction is clear and you should show up with a view)
```

**If your manager is a participant**, append:

```
## Leadership Signals
For each signal from your manager:
`- **[Signal type]:** What happened > what it signals`
```

Show the full proposed note. Do NOT write it yet.
Ask: "Write this meeting note?"

---

## Step 3 — Propose initiative updates

Read `context/initiatives/` to identify relevant initiative files.

For each relevant initiative, propose in diff format:

```
### Initiative: [name].md

**Running Narrative** — ADD at top:
> [YYYY-MM-DD] [Thread: label if sub-topic] — [2-3 sentence summary]

**Key Decisions** — ADD if a decision was made:
> | [YYYY-MM-DD] | [Decision] | [Meeting: title] |

**Open Action Items** — ADD new or MARK COMPLETE as applicable
```

If no initiative is clearly relevant, say so and skip.

Show all proposals. Do NOT write yet.
Ask: "Apply these initiative updates?"

---

## Step 4 — Propose context file updates

Review the context file loaded in Step 1 (if any). If the meeting revealed something
that should update it (changed cadence, new recurring participant, new standing agenda
item), propose:

```
### Context file: meetings/_context/[file].md

**Section: [name]**
CHANGE:
> [current text]
TO:
> [proposed text]
REASON: [why]
```

If nothing warrants an update, say so explicitly.

Show proposals. Do NOT write yet.
Ask: "Apply these context file updates?"

---

## Step 5 — Write on confirmation only

Write each piece only after explicit confirmation:
1. Meeting note → after confirming Step 2
2. Initiative updates → after confirming Step 3
3. Context file updates → after confirming Step 4

Each gate is independent. Never auto-write anything.
