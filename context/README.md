# context/

Standing context that Claude loads during work sessions.

---

## What goes here

| File / Folder | Purpose |
|---|---|
| `initiatives/` | One file per active initiative. This is the vault spine — the primary source of truth for what each product area is doing, what's been decided, and what's open. See `initiatives/README.md`. |
| `org-context.md` | Org structure, team roster, stakeholder map, reporting lines. |
| `working-principles.md` | How you think, your product instincts, communication patterns, standing directives from your manager. |
| `voice-samples.md` | Writing samples used by the `match-voice` skill for voice calibration. Auto-populated over time as you mark messages as final. |

---

## How Claude uses this

Files in this folder are loaded on demand, not all at once. The routing table in `_meta/context-routing.md` maps keywords and topics to specific files. Claude loads the relevant file when the topic comes up, not at session start.
