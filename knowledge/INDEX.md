# Knowledge INDEX

**How to use this file:** This is the routing layer. Read it completely at conversation start. Then load only the files relevant to the current task. Do not preload everything — context budgets matter.

---

## Directory Map

```
knowledge/
├── INDEX.md                    ← YOU ARE HERE (always load)
├── system-maintenance.md       ← Load when: auditing or maintaining the knowledge system
│
├── hypotheses/
│   ├── index.md                ← Load when: reviewing what's being tested, or graduating a hypothesis
│   ├── rejected.md             ← Load when: checking known false beliefs before starting work
│   └── EXAMPLE.md              ← Reference only — shows the schema
│
└── [your-files]                ← Add domain-specific files here as your system grows
```

---

## What to Load Per Task

| Task | Files to load (beyond this INDEX) |
|------|-----------------------------------|
| Review active hypotheses | `hypotheses/index.md` |
| Check known false beliefs | `hypotheses/rejected.md` |
| Audit knowledge system | `system-maintenance.md` |
| [Add your task types here] | [Add your files here] |

---

## Load-on-Demand Rules

1. **Never load more than 4 knowledge files at once** unless the task explicitly requires it.
2. **Expand this INDEX as your system grows** — add rows to the table above and entries to the directory map.
3. If a task doesn't fit any routing above, flag it and ask before loading speculatively.

---

## System Status

> **Last maintained:** [DATE]
> **Active hypotheses:** [N] — see `hypotheses/index.md`
> **Domains covered:** [LIST]
> **Next maintenance due:** [DATE or trigger condition]

---

## Notes for the Agent

- If you discover something this INDEX doesn't cover, flag it at end of task as a potential addition.
- This file should stay under 80 lines. If it grows beyond that, split or trim.
