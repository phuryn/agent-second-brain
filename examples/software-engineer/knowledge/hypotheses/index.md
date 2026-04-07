# Hypothesis Index

---

## Active Hypotheses

### HYP-006
**Statement:** PRs that include a "testing strategy" section in their description get fewer post-merge bugs than those without, even when test coverage is similar.
**Status:** active
**Created:** 2026-03-10
**Context:** Backend PRs with >200 lines changed
**Evidence for:**
- 2026-03-10 Payments refactor: had testing strategy, zero post-merge issues
- 2026-03-18 Auth migration: had testing strategy, caught edge case in review that tests missed
**Evidence against:**
- [none yet]
**Notes:** Need 1 more data point. Tracking all PRs >200 lines.

### HYP-008
**Statement:** Database queries that join more than 3 tables degrade noticeably (>200ms p99) once any joined table exceeds 1M rows.
**Status:** active
**Created:** 2026-03-22
**Context:** PostgreSQL 15, current indexing strategy
**Evidence for:**
- 2026-03-22 Analytics dashboard: 4-table join hit 450ms p99 after user_events passed 1.2M rows
**Evidence against:**
- [none yet]
**Notes:** Monitoring three more queries that are approaching the threshold.

---

## Graduated Hypotheses

### HYP-002
**Statement:** Non-backward-compatible database migrations cause rollback failures more than 50% of the time.
**Status:** graduated
**Graduated:** 2026-02-01
**Now lives in:** `knowledge/architecture-decisions.md` as AD-02
**Evidence summary:** 3 rollback failures out of 4 non-backward-compatible migrations in Q3-Q4 2025.

### HYP-004
**Statement:** Generic error wrapping adds 30+ minutes to debugging sessions when errors cross package boundaries.
**Status:** graduated
**Graduated:** 2026-02-20
**Now lives in:** `knowledge/review-patterns.md` as R2
**Evidence summary:** 5 debugging sessions tracked. Average added time: 35 minutes. All involved wrapped errors crossing 2+ package boundaries.

---

## Rejected Hypotheses

### HYP-005
**Statement:** Requiring two approvals on all PRs reduces post-merge bugs compared to one approval.
**Status:** rejected
**Rejected:** 2026-03-01
**Reason:** Tracked 40 PRs over 6 weeks. Bug rate was identical (7.5% vs 8%). Second reviewer mostly rubber-stamped after seeing the first approval.
**Notable finding:** The quality of the review matters more than the count. Better signal: require domain-expert approval for PRs touching specific subsystems.
