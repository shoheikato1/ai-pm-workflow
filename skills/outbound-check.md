# Skill: outbound-check

**Auto-triggered.** Runs on every outbound draft before it leaves your hands: Slack messages, documents, meeting prep, shared artifacts.

---

## Why this exists

Performance feedback from a manager is easy to note and forget. This skill operationalizes it into a system check so it runs automatically instead of relying on memory or discipline.

The two behavioral patterns this enforces:
1. **Activity to impact:** tie every piece of communication to an outcome, not just visibility
2. **Vocabulary consistency:** use the team's accepted language, not generic or AI-sounding alternatives

---

## How it runs

1. Draft the output using voice and writing rules
2. Run every item in the relevant section below against the draft
3. Fix what fails silently
4. Flag anything that requires factual verification with [CHECK]
5. Show the Checklist Report after the output — never skip it

---

## Before Sending a Slack Message

* [ ] Does every term match the team's accepted vocabulary? Check the glossary or recent docs if unsure — don't guess
* [ ] Did I lead with what I'm offering or sharing, not what I need?
* [ ] Is there enough context that the reader can respond immediately without asking a follow-up?
* [ ] Is the ask clear? Can they answer yes/no or take one action?
* [ ] Would this land the same way if I read it from the recipient's perspective?
* [ ] Tone: does this sound like "here's how I can help" or "I need something from you"?

---

## Before Sharing a Document or Brief

* [ ] Every factual claim verified against source material — nothing from memory alone
* [ ] Accepted vocabulary used throughout — no generic or AI-sounding alternatives
* [ ] Key point lands in 10 seconds of skimming
* [ ] Concrete examples included — real scenarios, not abstract groupings
* [ ] Success defined upfront: who uses this, what behavior should change, how we measure it
* [ ] Anything uncertain flagged with [CHECK] before sharing

---

## Before a Meeting

* [ ] Read the agenda — know what's being discussed before walking in
* [ ] Reviewed the relevant context file or reference doc for current state
* [ ] Prepared 1-2 points where I can add value: unblock someone, connect dots, surface a risk
* [ ] Contributions framed as "here's what I can help with," not "here's what I need"

---

## Before Sharing Any AI-Generated Output

* [ ] Read every line — every claim, every name, every reference verified against source
* [ ] Accepted vocabulary confirmed throughout
* [ ] Removed anything that sounds like AI filler or generic framework language
* [ ] Would I defend every sentence if someone asked where it came from?

---

## Checklist Report Format

Show after every draft. Never skip.

```
--- Checklist Report ---
Type: [Slack / Document / Meeting Prep / Artifact]

[PASS] Vocabulary confirmed against glossary
[PASS] Leads with value, not an ask
[FIXED] Added context so recipient can respond without follow-up
  > Before: "Can you check the pipeline?"
  > After: "The extraction job for [account] is showing [X]. Can you confirm whether [Y]?"
[CHECK] Factual claim needs verification: "[specific claim]"

Result: 3/4 passed, 1 fixed, 1 flagged
---
```

**[PASS]** = check passed, no change needed
**[FIXED]** = check failed, fixed automatically — show before/after
**[CHECK]** = cannot verify automatically — you must confirm before sending
