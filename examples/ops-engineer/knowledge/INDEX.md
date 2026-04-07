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
├── incident-patterns.md          ← Load when: responding to or reviewing an incident
├── health-baselines.md           ← Load when: evaluating system health or setting alerts
└── runbooks/                     ← Load the relevant service file when needed
    ├── api-gateway.md
    ├── data-pipeline.md
    └── auth-service.md
```

---

## What to Load Per Task

| Task | Files to load (beyond this INDEX) |
|------|-----------------------------------|
| Incident response or postmortem | `incident-patterns.md` |
| Runbook execution or update | `runbooks/[service].md` |
| Health review or alert tuning | `health-baselines.md` |
| Hypothesis review | `hypotheses/index.md` |
| Audit knowledge system | `system-maintenance.md` |

---

## Load-on-Demand Rules

1. Never load more than 4 knowledge files at once.
2. Load only the specific runbook for the service in question — not all runbooks.
3. `incident-patterns.md` and `health-baselines.md` should rarely be loaded together; if they are, confirm this is intentional.

---

## System Status

> **Last maintained:** 2026-04-01
> **Active hypotheses:** 2 — see `hypotheses/index.md`
> **Services covered:** API gateway, data pipeline, auth service
> **Next maintenance due:** 2026-05-01
