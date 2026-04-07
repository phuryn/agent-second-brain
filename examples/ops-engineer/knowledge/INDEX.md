# Knowledge INDEX

**How to use this file:** This is the routing layer. Read it completely at conversation start. Then load only the files relevant to the current task. Do not preload everything — context budgets matter.

---

## Directory Map

```
knowledge/
├── INDEX.md                       ← YOU ARE HERE (always load)
├── system-maintenance.md          ← Load when: auditing or maintaining the knowledge system
├── incident-patterns.md           ← Load when: responding to or reviewing incidents
├── health-baselines.md            ← Load when: capacity planning or anomaly detection
│
├── runbooks/
│   ├── api-gateway.md             ← Load when: incident involves API gateway
│   ├── data-pipeline.md           ← Load when: incident involves data pipeline
│   └── auth-service.md            ← Load when: incident involves authentication
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
| Active incident | `incident-patterns.md` + relevant `runbooks/*.md` |
| Post-incident review | `incident-patterns.md`, `health-baselines.md` |
| Capacity planning | `health-baselines.md` |
| Review active hypotheses | `hypotheses/index.md` |
| Audit knowledge system | `system-maintenance.md` |

---

## Load-on-Demand Rules

1. **Never load more than 4 knowledge files at once** unless the task explicitly requires it.
2. **Expand this INDEX as your system grows** — add rows to the table above and entries to the directory map.
3. If a task doesn't fit any routing above, flag it and ask before loading speculatively.

---

## System Status

> **Last maintained:** 2026-04-01
> **Active hypotheses:** 2 — see `hypotheses/index.md`
> **Domains covered:** incident response, platform reliability, capacity planning
> **Next maintenance due:** When active hypotheses exceed 10 or any file exceeds 400 lines
