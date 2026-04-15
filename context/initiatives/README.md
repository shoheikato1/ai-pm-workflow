# context/initiatives/

One file per active initiative. This is the spine of the vault.

Every meeting note, decision, and action item eventually traces back to an initiative file. The running narrative at the top of each file is the fastest way to catch up on any product area without reading through meeting notes.

---

## File structure

Each initiative file follows the template in `templates/initiative.md`:

* **Running Narrative** — most recent entry at top, newest-first. 2-3 sentences per entry.
* **Key Decisions** — a table of decisions with date, decision, and source.
* **Positions and Stances** — cross-team boundary calls and explicit stances taken.
* **Open Action Items** — unchecked items across all related meetings.
* **Open Questions** — unresolved questions that affect direction.

---

## Folder organization (optional)

For larger portfolios, organize by domain:

```
initiatives/
├── [domain-a]/
│   ├── [initiative-1].md
│   └── [initiative-2].md
├── [domain-b]/
│   └── [initiative-3].md
└── cross-team/
    └── [shared-initiative].md
```

---

## Getting started

Copy `templates/initiative.md` for each active product area you own.
Add a row to `_meta/context-routing.md` so Claude knows when to load it.
