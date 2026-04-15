# Memory Index

Persistent memory files that survive context window resets.
Each entry is a separate file in this directory. This index is loaded every session.

---

## How it works

Memory files capture things Claude should know across all sessions that are not derivable from reading current files:

* Your preferences and working style
* Feedback you've given on Claude's behavior (what to stop doing, what to keep doing)
* Project context that changes over time (decisions made, priorities shifted)
* Pointers to where things live in external systems

Each memory is a separate `.md` file with a one-line summary here in the index.

---

## Index

*(empty — add entries as patterns emerge)*

---

## When to save a memory

Save a memory when:
* You correct Claude's behavior and want it not to repeat the mistake
* Claude does something exactly right that wasn't obvious — confirm it and log it
* You learn something about a project that isn't in any file but will matter next week
* You establish a preference that should apply across all future sessions

Do not save memories for things already documented in files or derivable from reading the vault.
