# AI-Augmented PM Workflow

I built this because the standard AI workflow for PMs doesn't actually work.

Every session starts from scratch. You re-explain your initiatives, your stakeholders, your open threads. The AI gives you generic professional language instead of yours. Meeting notes get written and forgotten. Nothing compounds.

I'm a Staff PM on a data platform team. My work spans 7+ cross-functional teams, a dozen active initiatives, and constant context-switching between technical discussions and stakeholder communication. I needed an AI that already knew all of that before I said a word.

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
├── skills/                     # Skill scripts (markdown, trigger-activated)
├── templates/                  # Meeting note and initiative templates
├── _meta/                      # Vault health: routing table, friction log, signal log
├── _staging/                   # Output staging (confirmed before final write)
└── memory/                     # Persistent memory across sessions
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
