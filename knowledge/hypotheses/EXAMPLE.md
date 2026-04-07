# Example Hypothesis Entries

This file shows what a well-formed hypothesis looks like at each stage of its lifecycle. Do not use this for actual hypotheses — it's a reference only. When adding a real hypothesis, add it to `index.md`.

---

## Example: Active Hypothesis

### HYP-007
**Statement:** Code review comments that cite a specific past incident where the pattern caused a failure get addressed in the same PR 3x more often than comments that cite general best practice.
**Status:** active
**Created:** 2026-02-14
**Context:** Backend codebase, senior engineer reviewees, synchronous review process

**Evidence for:**
- 2026-02-14 Auth PR: cited the 2025-11 token leak incident → fix included in same PR
- 2026-03-01 DB migration PR: cited the 2025-08 timeout incident → addressed immediately

**Evidence against:**
- 2026-02-28 Cache PR: cited a past incident → reviewer disagreed the pattern was the same; fix deferred
  - Note: Incident cited was from a different system. May be a confounding factor.

**Notes:** Need 1 more clean data point before graduation. Testing with incidents from the same service only.

---

## Example: Graduated Hypothesis

### HYP-003
**Statement:** Experiment run times under 72 hours produce higher variance results than runs over 7 days for this user cohort.
**Status:** graduated
**Graduated:** 2026-01-20
**Now lives in:** `knowledge/experiment-standards.md` as Rule: "Minimum run time: 7 days for behavioral metrics"

**Evidence summary:** 5 experiments over 10 weeks. Sub-72h runs averaged ±18% variance; 7d+ runs averaged ±6%. One exception on a major product launch (external factor) — excluded from rule scope with a note.

---

## Example: Rejected Hypothesis

### HYP-011
**Statement:** Adding explicit rollback steps to incident runbooks reduces mean time to recovery by 30%+.
**Status:** rejected
**Rejected:** 2026-03-15
**Reason:** Tracked 8 incidents over 6 weeks. 5 had explicit rollback steps available; recovery time was indistinguishable from those without. Engineers reported skipping the rollback steps in 3 of 5 cases because the situation diverged from the runbook scenario.

**Notable finding:** Rollback steps were followed only when the incident matched the runbook scenario closely. The limiting factor is runbook applicability, not rollback step presence. This reframes the problem: better incident classification, not more detailed runbooks.
