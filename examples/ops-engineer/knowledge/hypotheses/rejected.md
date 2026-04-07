# Rejected Hypotheses — Immune Memory

Beliefs that were tested and proven wrong. The agent reads this file to avoid re-testing dead ideas.

---

### HYP-002 — Rollback steps reduce MTTR by 30%+
**Was:** Adding explicit rollback steps to incident runbooks reduces mean time to recovery by 30%+.
**Evidence against:** 8 incidents over 6 weeks. Engineers skipped rollback steps in 3/5 cases because the situation diverged from the runbook.
**Key learning:** Runbook applicability is the bottleneck, not rollback detail. Better incident classification > more detailed runbooks.
**Rejected:** 2026-03-15
