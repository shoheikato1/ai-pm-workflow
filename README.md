# AI-Augmented PM Workflow

I built this because the standard AI workflow for PMs doesn't actually work.

Every session starts from scratch. You re-explain your initiatives, your stakeholders, your open threads. The AI gives you generic professional language instead of yours. Meeting notes get written and forgotten. Nothing compounds.

I work across a portfolio of AI agent products: voice agents that handle live customer calls, conversational SMS agents, signal intelligence products. On any given day I'm moving between deep technical discussions and executive stakeholder communication across 7+ teams. I needed an AI that already knew all of that before I said a word.

This repo is a sanitized template of the system I actually use.

---

## What It Is

A vault-based operating system built on [Obsidian](https://obsidian.md), [Claude Code](https://claude.ai/code), and git.

* **CLAUDE.md** is the session contract. It tells Claude who I am, what I'm working on, how I communicate, and what to load before responding. It's reread at the start of every session.
* **Skills** are markdown workflows triggered by phrases. "Ingest this meeting" runs a 5-step structured process. "Morning brief" surfaces open actions and today's context. No re-explaining required.
* **Session Handover** carries state forward. 30-line cap. Overwritten each session. Every session starts mid-thought, not from scratch.
* **The vault** is the source of truth. 23 initiative files. 28+ meeting notes. A running decision log, action item tracker, and stakeholder conversation thread — all maintained automatically.

---

## The Design Decisions That Actually Matter

### Confirmation gates everywhere
Claude proposes. I confirm. Nothing writes without explicit approval. Each gate is independent.

This sounds like friction. It's the opposite. An AI that auto-writes will corrupt your vault with confident errors faster than you can clean them up. The gate keeps me in control of the record while removing the cognitive load of writing it.

### Skills are plain markdown, not prompts
Skills are `.md` files I can read, edit, and debug. They're not stored in a tool, not wrapped in an API, not locked to any platform. If a skill produces the wrong output, I open the file and fix the step. The system is fully transparent.

### The session handover is 30 lines, no more
When the handover gets longer than 30 lines, it stops being useful. The rule forces discipline: the vault carries depth, the handover carries the thread. What's open, what just happened, what carries forward tomorrow. That's it.

### Voice calibration, not AI polish
The `match-voice` skill loads my own past writing as examples before drafting anything. It's looking for register, sentence length, directness, and whether the ask lands at the end where it should. Generic professional language is the wrong target. My voice is the target.

### The PM Translation Layer
Every technical meeting note includes a section I call the PM Translation Layer: what the technical discussion meant in PM terms, and the injection points for the next meeting — moments where engineers made scope calls that warrant PM input. This keeps me from walking into follow-up meetings having processed the transcript but not the implications.

---

## Two Design Patterns Worth Stealing

### Initiative files with a running narrative

Every product area I own has a single file in `context/initiatives/`. The top of each file is a running narrative: 2-3 sentence entries, newest first, one per significant development.

When a meeting touches an initiative, Claude proposes an addition to the running narrative as part of the meeting ingest flow. Over time, each file becomes a living history of that product area: what happened, what was decided, what's in flight, where the sticking points are.

The practical benefit: Claude can brief itself on any initiative in seconds without reading through a month of meeting notes. And I can do the same.

The structure for each file:

```
## Running Narrative        ← newest entry at top, updated after every relevant meeting
## Key Decisions            ← table: date | decision | source
## Positions and Stances    ← where the team drew a boundary or took an explicit cross-team stance
## Open Action Items        ← aggregated across all related meetings
## Open Questions           ← unresolved questions that affect direction
```

The "Positions and Stances" section is the one most people skip. It's the most valuable. Cross-team scope decisions, declined ownership calls, explicit stances — these come up again in future meetings. Having them in one place means I'm never relitigating a decision that was already made.

### Meeting context files

Each recurring meeting has a standing context file in `meetings/_context/`. Before generating a note for that meeting, Claude loads the matching context file.

A context file captures things that don't change meeting to meeting: the purpose of the meeting, the recurring participants and their roles, standing agenda items, past decisions that remain relevant, and things to watch for from specific stakeholders.

The result: Claude walks into every recurring meeting already briefed. The generated note reflects that context instead of treating each meeting as if it happened in isolation.

For a weekly sync with an important stakeholder, the context file might include: their current priorities, the decisions that came out of the last three sessions, the open thread they keep returning to, and what they're evaluating you on. That's not something you want to re-explain each session.

---

## The Self-Improvement Loop

This is the part that surprised me most.

Every daily summary skill runs a friction scan: moments where I said "that's wrong," where the wrong context was loaded, where something had to be re-explained from the previous session. Those get logged to `_meta/friction.md` with a root cause and a proposed fix.

The friction log now has 128 lines of entries. Each one became a change: a routing rule added, a skill step clarified, a context file created. Over ~4 weeks of active use, the system made itself measurably better at knowing when to load which file, how to frame which output, and when not to guess.

Real example: Claude was paginating through 1,400+ Slack users to find a DM contact instead of checking the channel index file that already had the ID. One friction log entry. One routing rule added to CLAUDE.md. Never happened again.

The system learns from its own errors because the errors are documented in a format that feeds back into the instructions.

---

## What It's Connected To

This system is designed to pull live data rather than rely on copy-paste:

| MCP Server | What it enables |
|---|---|
| Meeting transcripts | Auto-fetch, parse, and file notes without ever leaving the vault |
| Jira | Sprint prep, ticket lookup, delivery planning |
| Slack | Channel history, drafting and sending messages |
| Google Drive | Document reads with session-safe token caching |
| Data catalog | Asset lookup during technical discussions |

Without MCP the system still works — you paste content in. MCP removes the copy-paste step.

---

## Structure

```
ai-pm-workflow/
├── CLAUDE.md                   # Session contract: who you are, rules, skill triggers
├── SESSION-HANDOVER.md         # Cross-session state (30-line cap, overwritten each session)
│
├── context/
│   ├── initiatives/            # One file per active initiative (the vault spine)
│   ├── org-context.md          # Org structure, stakeholder map
│   └── working-principles.md   # How you think, standing directives
│
├── meetings/
│   └── _context/               # Standing files loaded before recurring meetings
│
├── people/                     # Per-person and per-team context files
├── working/                    # In-progress drafts and working docs
│
├── skills/                     # Skill scripts (markdown, trigger-activated)
├── templates/                  # Meeting note and initiative templates
└── _meta/                      # Vault health: routing table, friction log, signal log
```

---

## Skills Included

| Skill | Trigger | What it does |
|---|---|---|
| `morning-brief` | "morning brief", "what's on my plate" | Surfaces open actions, recent decisions, today's meetings |
| `meeting-ingest` | "ingest this meeting" | Fetches transcript, generates structured note, proposes initiative updates |
| `match-voice` | "draft this", "how should I say this" | Calibrates output to your writing voice, not AI voice |
| `daily-summary` | "let's wrap up", "EOD" | Synthesizes the day, surfaces friction, proposes system improvements |

---

## How to Adapt This

1. Fork or copy this repo
2. Edit `CLAUDE.md`: your name, role, org context, writing rules, MCP servers
3. Create your initiative files in `context/initiatives/` — one per active product area
4. Add your org context in `context/org-context.md`
5. Start logging voice samples in `context/voice-samples.md` (the match-voice skill gets more accurate over time)
6. Run Claude Code from the vault directory

The system is useful from day one but compounds over weeks. The more context accumulates, the less you explain.

---

## What This Signals (and What It Doesn't)

The point of this system is not the tooling. Any PM could set up Obsidian and Claude Code.

The point is applying the same product thinking to your own workflow that you'd apply to a product: identify the real pain, design around the failure mode, build a feedback loop, iterate. The friction log is a bug tracker for the system itself. The session handover is a product spec for the next session.

If you're a PM who thinks about AI seriously, I'm always interested in comparing notes: [linkedin.com/in/shoheikato](https://linkedin.com/in/shoheikato)

---

*Sanitized template. Company-specific content (initiative names, stakeholders, internal tools) has been removed. The structure, skills, and design rationale are real.*
