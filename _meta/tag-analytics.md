# Tag Analytics

Tracks which context files and skills get loaded each session. Used to evaluate whether the vault is working as intended and to decide what to keep, restructure, or archive.

---

## How to read this

* **High frequency + high usefulness** — hot file, keep accessible and well-maintained
* **High frequency + low usefulness** — loaded by habit but not contributing, investigate the routing rule
* **Low frequency + high usefulness** — deep reference, keep but don't expect it in every session
* **Never loaded** — candidate for archival or deletion

Same logic applies to skills: a skill that never gets triggered either has a broken trigger phrase or is solving a problem that doesn't actually recur.

---

## Session Context Loads (raw data, append per session)

| Date | Session | Files Loaded | Useful? | Notes |
|---|---|---|---|---|
| YYYY-MM-DD | [session-id] | [file1], [file2] | Yes / Partial / No | [what the session was about] |

---

## Weekly Digest

### Week of YYYY-MM-DD

| File | Times Loaded | Useful Rate | Action |
|---|---|---|---|
| context/initiatives/[name].md | 4 | High | Keep |
| skills/[name].md | 1 | Low | Review trigger phrase |
| context/[name].md | 0 | — | Archive candidate |
