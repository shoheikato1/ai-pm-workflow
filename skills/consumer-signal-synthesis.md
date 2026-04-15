# Skill: consumer-signal-synthesis

> Triggered automatically during cross-functional meetings. Scans for customer signals
> and synthesizes them into a running inventory tied to product decisions.

Trigger: any meeting with participants from multiple teams (GTM, design, leadership,
sales, customer success, marketing) or with 8+ attendees from different functions.

---

## Why this exists

Direct user interviews are one source of customer signal. Cross-functional meetings
are another — often richer, because they carry signal from people who talk to customers
every day: sales, CS, PMM, design research. This skill treats those meetings as a
customer insight channel and captures signal systematically instead of letting it
pass by.

---

## Step 1 — Scan the transcript

After generating the meeting note, scan the full transcript for:

* Customer feedback: what customers said, complained about, or asked for (exact quotes preserved)
* Onboarding friction: where new customers get stuck, drop off, or need help
* Conversion and churn signals: what's driving wins or losses
* UX and usability findings: design research results, usability patterns, A/B test outcomes
* PMM and positioning signals: how the product is being sold, competitive framing, messaging gaps
* Pricing and business model signals: what customers push back on, what they pay for without friction
* Any signal that connects to your product area, even indirectly

---

## Step 2 — For each signal found

Capture:

```
| Date | Meeting | Signal | Consumer reframe | Product question it answers |
```

* **Signal:** what was said or observed, with the closest available quote
* **Consumer reframe:** translate from internal/operational language to the experience of the person on the other end. Start from the human, not the system.
* **Product question:** which open product question does this answer, challenge, or complicate?

---

## Step 3 — Append to the signal inventory

Output path: `context/consumer-signal-inventory.md`

Add each signal as a new row. Preserve exact quotes. Do not paraphrase customer language — that's the signal.

If a signal is strong enough to warrant a dedicated entry (a quote that anchors a product decision, a pattern that's appeared 3+ times, a finding that changes prioritization): flag it for promotion. Don't auto-promote. Surface it.

---

## Step 4 — Note in the meeting summary

After the meeting note, add a one-line summary:

```
Consumer signals captured: [N] signals appended to consumer-signal-inventory.md
Most notable: [one-line description of strongest signal]
```

If nothing was captured: "No consumer signals surfaced in this meeting."

---

## Notes

* This step does not require confirmation. Append silently and mention what was captured.
* Preserve customer language exactly. The way a customer describes a problem is often more
  valuable than a clean paraphrase of it.
* Indirect signals count. A sales rep describing why a deal was lost is customer signal.
  A designer noting where users hesitated in a prototype is customer signal.
* Skip for internal-only meetings: standups, sprint ceremonies, 1:1s between engineers.
