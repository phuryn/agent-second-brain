# Knowledge INDEX

**How to use this file:** This is the routing layer. Read it completely at conversation start. Then load only the files relevant to the current task. Do not preload everything — context budgets matter.

---

## Directory Map

```
knowledge/
├── INDEX.md                       ← YOU ARE HERE (always load)
├── system-maintenance.md          ← Load when: auditing or maintaining the knowledge system
├── review-patterns.md             ← Load when: reviewing PRs or analyzing review feedback
├── architecture-decisions.md      ← Load when: proposing or evaluating architecture changes
├── bug-patterns.md                ← Load when: investigating bugs or post-incident analysis
│
└── hypotheses/
    ├── index.md                   ← Load when: reviewing what's being tested, or graduating a hypothesis
    ├── EXAMPLE.md                 ← Reference only — shows the schema
    └── rejected.md                ← Immune memory — beliefs proven wrong
```

---

## What to Load Per Task

| Task | Files to load (beyond this INDEX) |
|------|-----------------------------------|
| Code review | `review-patterns.md`, `architecture-decisions.md` |
| Bug investigation | `bug-patterns.md`, `architecture-decisions.md` |
| Architecture proposal | `architecture-decisions.md` |
| Review active hypotheses | `hypotheses/index.md` |
| Audit knowledge system | `system-maintenance.md` |

---

## Load-on-Demand Rules

1. **Never load more than 4 knowledge files at once** unless the task explicitly requires it.
2. **Expand this INDEX as your system grows** — add rows to the table above and entries to the directory map.
3. If a task doesn't fit any routing above, flag it and ask before loading speculatively.

---

## System Status

> **Last maintained:** 2026-03-15
> **Active hypotheses:** 2 — see `hypotheses/index.md`
> **Domains covered:** code review, architecture, bug patterns
> **Next maintenance due:** When active hypotheses exceed 10 or any file exceeds 400 lines
