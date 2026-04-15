# Skill: morning-brief

> Triggered at the start of the day. Surfaces recent context, collects open
> action items, and shows today's meetings.

Trigger phrases: "morning brief", "to-do", "what's my to-do", "what's on my plate"

---

## Step 0 — Determine date

Read date from system context. Do not ask. If a specific date is stated
in the trigger, use that instead.

---

## Step 1 — Recent developments lookback

Determine lookback source:
* **Monday or Tuesday-after-holiday** → read last week's `weekly/YYYY-WXX.md`.
  If no weekly file exists, fall back to last week's daily notes.
* **Any other day** → read yesterday's `daily/YYYY-MM-DD.md`.

If the file is missing: note it and skip.

Summarize in 3-5 bullets:
* Decisions made
* Initiatives that moved
* Open threads still in play

---

## Step 2 — Collect open action items

Read:
* `TODO.md` — extract all unchecked `- [ ]` items
* All `context/initiatives/*.md` files — extract unchecked `- [ ]` action items
* The last 5 meeting files in `meetings/` — extract unchecked action items
* Yesterday's daily note (if available) — extract any unchecked items

Deduplicate across sources. If the same item appears in multiple places,
list it once and note the source.

---

## Step 3 — Present to-do list

Group collected action items by initiative. For items that don't map to a
named initiative, group under **Standalone**.

Present the full list. Then ask:
"Anything on this list already done?"

---

## Step 4 — Mark completions

For each item confirmed as done:
* Confirm: "Mark [item] as complete in [source file]?"
* Only write after explicit confirmation for each one
* Change `- [ ]` to `- [x]` in the source file

Do not batch-mark without per-item confirmation.

---

## Step 5 — Today's meetings

> If you have a calendar MCP connected, fetch today's events. Otherwise, skip
> or prompt the user to paste their schedule.

Show: Time | Title | Duration | Attendees (if available)

Filter out: all-day events, declined events, personal/non-work events
unless they seem relevant.

For any meeting that has a matching context file in `meetings/_context/`,
note it: "(context file available)"

This step is read-only. No writes.

---

## Notes

This skill updates existing files only. It never creates a new file.
Each write in Step 4 requires explicit per-item confirmation.
