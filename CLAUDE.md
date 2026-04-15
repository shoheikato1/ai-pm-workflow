# CLAUDE.md — Template

> Copy this file into your vault root. Fill in the bracketed sections.
> This file is the authoritative instruction set for Claude Code sessions.

---

## Who I Am

**[YOUR NAME]** ([your-email@company.com]). [Your title] on the [Your team] team at [Company].
Manager: [Manager name].

Org context and people directory: `context/org-context.md` | `people/`

---

## Writing Rules (hard, every output)

* **No em dashes.** Never use — in any output. Rewrite with commas, colons, or shorter sentences.
* **Bullet lists use * not -.** Avoid hyphenated compounds where alternatives exist.
* Voice calibration: run `skills/match-voice.md` when producing language I will send or share.

> Customize: add your own style rules here. Common ones: no passive voice, no hedging language,
> no "I hope this finds you well", prefer short sentences.

---

## Skill Triggers

| Trigger phrase | Skill |
|---|---|
| "morning brief" / "what's on my plate" | `morning-brief` |
| "ingest this meeting" / "let's process that meeting" | `meeting-ingest` |
| "draft this" / "how should I say this" / "clean this up" | `match-voice` |
| "let's wrap up" / "EOD" / "daily summary" | `daily-summary` |

> Add your own trigger phrases and skills here. See `skills/` for included skills.
> Full skill index: `skills/README.md`

---

## Session Operations

**SESSION-HANDOVER.md:** Update after every significant action (file written, decision captured,
skill executed). Keep the RESUME HERE block current. Max 30 lines. Overwrite each session, don't
append.

**Staging check (session start):** Check `_staging/` for files (excluding README.md). If any
exist, surface a warning immediately.

**Auto-staging:** Save substantial outputs to `_staging/YYYYMMDD-[type]-[slug].md` immediately.
Stage: meeting notes, drafts, briefs, analysis, multi-paragraph answers. Don't stage one-liners
or confirmations. On confirm: move to vault, delete staging file.

---

## Observability (always active)

**Signal log:** Append observations to `_meta/signal-log.md` at the end of each session.
Capture: corrections, wrong context loaded, pattern observations, voice calibration notes.

**Friction capture:** When output requires correction or the same info is re-explained, append
to `_meta/friction.md`.

**Context loading transparency:** When loading context files for a task, tell me which files
and why. This lets me correct misfires.

---

## Vault Conventions

* **File naming:** `YYYY-MM-DD` for dates, kebab-case for everything else
* **Frontmatter:** always include `date` and `tags`
* **Extract, don't summarize:** preserve signal, don't compress it
* **`context/initiatives/` is the spine:** each file synthesizes and links across all meetings

---

## MCP Connections (if configured)

> List your MCP servers here so Claude knows what data it can pull live.

| Service | Use for |
|---|---|
| [Meeting transcript tool] | Fetch and ingest meeting notes |
| [Project tracking tool] | Ticket lookup, sprint planning |
| [Messaging tool] | Channel history, drafting messages |

---

## Context Routing

When working on a topic, Claude should load the relevant context file before responding.

| Topic | File to load |
|---|---|
| [Initiative 1] | `context/initiatives/[initiative-1].md` |
| [Initiative 2] | `context/initiatives/[initiative-2].md` |
| [Stakeholder 1] | `people/[stakeholder-1].md` |
| [Recurring meeting] | `meetings/_context/[meeting-slug].md` |

> Full routing table: `_meta/context-routing.md`
