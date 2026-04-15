# What Building This Taught Me About AI Products

I didn't set out to learn anything. I built a workflow tool because the standard AI setup wasn't working for me, and I wanted something better.

But the problems I kept running into while building it turned out to be the same problems AI product teams are wrestling with at scale. Three in particular are worth writing down.

---

## 1. Personalization: examples beat rules

The first version of my voice calibration system was a list of writing rules in a config file. Short sentences. No hedging. Direct asks. All correct. All useless.

The output still sounded like an AI that had been told to write like a human. The rules described the target but couldn't capture the texture: the specific way I open a message, where I put the ask, how I acknowledge someone before getting into it.

The fix was obvious in retrospect: use my own sent messages as the calibration source instead of rules I wrote about those messages. Real examples carry signal that descriptions of examples can't. The model stopped trying to match an abstract profile and started matching actual instances.

The broader insight: personalization problems in AI products are almost always framed as preference capture problems. What does the user want? The harder question is fidelity: does the AI's output feel like it came from this specific person, in this specific context, for this specific relationship? Rules get you to "professional and clear." Examples get you to "sounds like her."

Any AI product trying to generate on behalf of a user (drafts, summaries, responses) will hit this wall. The teams that crack it will do it with behavioral signal, not stated preferences.

---

## 2. LLM eval: you can't improve what you can't see

For weeks, I had no idea which context my AI was actually loading before responding. It would pull the wrong initiative file, miss a relevant stakeholder doc, or skip a context file that should have been obvious. I'd get a subtly wrong answer and have no way to trace why.

So I built a log. Every file load, every session: which file, which task, what triggered it. A second layer tracked frequency and usefulness across weeks, so I could see patterns: files loaded constantly but never useful, files never loaded that should have been, trigger rules that were misfiring.

The first few weeks of data were humbling. The model was routing confidently to the wrong context on a consistent basis. I wouldn't have known without the log.

The broader insight: most AI products ship without meaningful observability into what the model is actually doing at inference time. Teams measure outputs (was the answer good?) but not inputs (was the context right?). Those are different problems. A model working perfectly on bad context will produce bad answers, and you'll optimize the wrong thing.

Context quality is the eval problem nobody talks about enough. Retrieval accuracy, routing decisions, what gets included and excluded: these are product decisions with measurable outcomes. Instrument them like you would any product surface.

---

## 3. Feedback loops: errors need somewhere to go

The self-improvement loop in this system came from a frustration: I'd correct something, Claude would get it right for the rest of the session, and then it would make the same mistake two sessions later. Nothing was accumulating.

The fix was treating errors as first-class artifacts. Every correction gets logged with a root cause and a proposed fix to the instructions. The daily summary skill surfaces those entries and proposes changes. Fixes get applied. The system gets better at a rate that compounds.

One concrete example: the model was paginating through 1,400 Slack users to find a contact instead of checking a channel index file that already had the ID. Logged it, added a routing rule, never happened again. That fix has held across dozens of sessions.

The broader insight: most AI products treat user corrections as training signal for a future model version, something that helps the next release but not this conversation. The compounding is slow and invisible to the user. There's a real product opportunity in making feedback loops tighter and more legible: here's what changed, here's why, here's what's different now. Users who can see the system improving are more likely to invest in correcting it.

This is the unsexy version of RLHF. It works at personal scale. I think it scales further than most teams assume.

---

## 4. Feedback loops apply to your own behavior too

My manager gave me specific behavioral feedback: tie work to measurable outcomes, not just activity. Use the team's vocabulary consistently. The kind of feedback that's easy to nod at and gradually forget.

Instead of writing it on a sticky note, I wired it into the system. Every outbound message — every Slack, every document, every meeting prep — runs through an automated checklist before it goes out. Vocabulary confirmed against the team glossary. Leading with value, not an ask. Enough context that the recipient can respond without a follow-up. The checklist shows a report every time: what passed, what was fixed, what needs my verification.

The feedback is now a system property, not a personal reminder.

The broader insight: PMs spend a lot of energy building feedback loops into products. Activation rates, support tickets, NPS. The same principle applies to your own communication. If a behavior needs to change, instrument it. Make the check automatic. The goal is to stop relying on willpower and start relying on the system.

There's also a second-order effect: when your communication system runs a vocabulary check on every message, you're forced to maintain a shared glossary. That glossary becomes a living artifact of how the team actually talks about the product, which is different from how the product is documented, which is different from how it's sold. Those gaps are often where the most important product problems live.

---

## The through-line

None of these were insights I read somewhere. They came from building something small and watching it fail in specific ways.

The personalization problem, the context quality problem, the feedback loop problem: none of these are research problems. They're product problems. They show up at the level of one user's workflow just as clearly as they show up at the level of a million users. The solutions at both scales rhyme more than most people expect.

If you're working on any of this, I'd like to compare notes: [linkedin.com/in/shohei-kato](https://linkedin.com/in/shohei-kato)
