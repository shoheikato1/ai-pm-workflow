# Skill: match-voice

**Purpose:** Calibrate any draft to sound like you, not like an AI. Used whenever
drafting a Slack message, cleaning up language in a document, or writing anything
on your behalf.

---

## When to run this skill

* Drafting a Slack message from scratch
* Cleaning up or rewriting language in a document or message
* You say "write this for me", "draft this", "clean this up", "how should I say this"
* Any output that will be sent or shared under your name

---

## Steps

**1. Load voice samples**

Read `context/voice-samples.md`. Find the sample(s) closest to the current task by type:
* Slack request: asking someone for time, input, or a favor
* Slack acknowledgment: accepting feedback, owning a mistake, confirming next steps
* Slack update: sharing status or progress without a specific ask
* Slack pushback: disagreeing or redirecting, diplomatically
* Doc framing: opening a section, positioning a decision, framing a tradeoff
* Doc summary: distilling findings or status for a skimming reader

If no close match exists yet, proceed with the writing rules in CLAUDE.md and note
that a sample of this type is still needed.

**2. Apply mode: Slack or document**

Slack:
* Warm and human. This is a request or a relationship moment, not a status report.
* Short sentences. No nested clauses.
* Get into it quickly. No "I hope this finds you well" or similar openers.
* Own uncertainty or mistakes directly and plainly.
* If there's a specific ask, make it clear at the end, not buried in the middle.

Document:
* Facts and logic drive the content. Your judgment shows in structure and sequencing.
* Write for a skimming reader. Key point should land in the first sentence of each section.
* Plain language. Replace jargon with what actually happens in practice.
* Still sounds like a person, not a spec, not a legal document.

**3. Calibrate against the closest sample**

After drafting, compare against the closest voice sample:
* Does the opening match your register?
* Are sentences roughly the same length?
* Does the ask or point land with the same directness?
* Does it sound like something you would actually send, or does it still sound like AI cleaned it up?

If it reads as AI-generated: simplify. Cut hedging language. Make it more direct.

**4. Final check**

Read the draft out loud (mentally). If it sounds like it could appear in a company
policy document, it needs another pass. If it sounds like you talking to a colleague
you respect, it's ready.

---

## Voice Sample Auto-Capture (always active)

Any time you say "this is what I'm sending", "going with this", or share a message
you have already sent: silently log it to `context/voice-samples.md` with a one-line
context note (who it was to, what type of message). No interruption. Just capture.

Only final approved or sent outputs count as samples. Draft inputs do not.

---

## Notes

* Voice samples accumulate over time. The more samples, the more precise the calibration.
* If `context/voice-samples.md` does not exist yet, create it and start capturing from today.
