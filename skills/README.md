# Skills

Skills are markdown files that Claude follows as step-by-step workflows.
Each skill is triggered by a phrase, executes a structured process, and gates
every write on explicit confirmation.

---

## Included Skills

| File | Trigger phrases | What it does |
|---|---|---|
| `morning-brief.md` | "morning brief", "what's on my plate", "to-do" | Surfaces open actions, recent decisions, today's meetings |
| `meeting-ingest.md` | "ingest this meeting", "process that meeting" | Generates structured meeting note, proposes initiative updates |
| `match-voice.md` | "draft this", "how should I say this", "clean this up" | Calibrates any draft to your writing voice |
| `daily-summary.md` | "let's wrap up", "EOD", "daily summary" | Synthesizes the day, surfaces friction, proposes system improvements |

---

## How Skills Work

1. You say a trigger phrase
2. Claude loads the matching skill file
3. Claude executes each step in order, showing proposed output
4. Claude asks for confirmation before writing anything
5. You confirm, adjust, or skip each gate independently

Skills are plain markdown. Edit them directly to change behavior, add steps,
or adjust the output format.

---

## Adding Your Own Skills

Create a new `.md` file in this directory. Add a trigger phrase in `CLAUDE.md`
under the Skill Triggers table. That's it.

Useful skills to build for your context:
* `weekly-rollup.md` — end-of-week synthesis and planning
* `sprint-prep.md` — pull sprint tickets, surface dependencies, write a brief
* `stakeholder-update.md` — generate a status update for a specific person
* `prep-[meeting-name].md` — load context and prepare talking points before a recurring meeting
