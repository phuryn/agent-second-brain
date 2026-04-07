# Hypothesis Index

---

## Active Hypotheses

### HYP-003
**Statement:** Incidents that occur within 2 hours of a deploy are 4x more likely to be caused by the deploy than by organic load changes.
**Status:** active
**Created:** 2026-03-15
**Context:** All production services, deploys during business hours
**Evidence for:**
- 2026-03-15 Auth service outage: deploy at 14:00, incident at 14:45, root cause was deploy
- 2026-03-28 API gateway latency spike: deploy at 10:30, incident at 11:15, root cause was new rate limit config
**Evidence against:**
- 2026-04-01 Pipeline lag: deploy at 09:00, lag spike at 10:30, but root cause was unrelated marketing campaign
**Notes:** 2 for, 1 against. Need more data before concluding. The counter-example may be an edge case (external traffic spike coinciding with deploy).

### HYP-004
**Statement:** Running canary deploys on the auth service for 30 minutes before full rollout would have caught 80%+ of auth-related incidents.
**Status:** active
**Created:** 2026-04-01
**Context:** Auth service deploys specifically
**Evidence for:**
- Retroactive analysis of IP-03 occurrences: both would have shown elevated CPU in canary
**Evidence against:**
- [none yet]
**Notes:** Cannot test retroactively with confidence. Proposing a canary pipeline for next quarter.

---

## Graduated Hypotheses

### HYP-001
**Statement:** Auto-scaling at 70% CPU utilization balances cost and response time better than 60% or 80% thresholds.
**Status:** graduated
**Graduated:** 2026-02-15
**Now lives in:** `knowledge/health-baselines.md` as Rule C1
**Evidence summary:** 3-week A/B test across API gateway instances. 60% wasted 25% more compute. 80% caused 3 latency breaches.

---

## Rejected Hypotheses

### HYP-002
**Statement:** Adding explicit rollback steps to incident runbooks reduces mean time to recovery by 30%+.
**Status:** rejected
**Rejected:** 2026-03-15
**Reason:** 8 incidents tracked. Engineers skipped rollback steps in 3 of 5 cases because the situation diverged from the runbook scenario.
**Notable finding:** The limiting factor is runbook applicability, not rollback detail. Better incident classification helps more than more detailed runbooks.
