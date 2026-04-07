# Knowledge INDEX

**How to use this file:** Read completely at conversation start. Load only what the task requires.

---

## Directory Map

```
knowledge/
├── INDEX.md                      ← YOU ARE HERE (always load)
├── system-maintenance.md         ← Load when: auditing the knowledge system
│
├── hypotheses/
│   ├── index.md                  ← Load when: reviewing or graduating a hypothesis
│   └── EXAMPLE.md                ← Reference only
│
├── review-patterns.md            ← Load when: doing a code review
├── architecture-decisions.md     ← Load when: evaluating or proposing system design
└── bug-patterns.md               ← Load when: doing a bug autopsy or incident analysis
```

---

## What to Load Per Task

| Task | Files to load (beyond this INDEX) |
|------|-----------------------------------|
| Code review | `review-patterns.md` |
| Architecture proposal / evaluation | `architecture-decisions.md` |
| Bug autopsy / post-incident | `bug-patterns.md` |
| Hypothesis review | `hypotheses/index.md` |
| Audit knowledge system | `system-maintenance.md` |

---

## Load-on-Demand Rules

1. Never load more than 4 knowledge files at once.
2. `bug-patterns.md` and `architecture-decisions.md` are dense — load only when the task requires them directly.

---

## System Status

> **Last maintained:** 2026-03-15
> **Active hypotheses:** 3 — see `hypotheses/index.md`
> **Domains covered:** API design, distributed systems, code review
> **Next maintenance due:** 2026-04-15
