# Rejected Hypotheses — Immune Memory

Beliefs that were tested and proven wrong. The agent reads this file to avoid re-testing dead ideas.

---

### HYP-005 — Two approvals reduce post-merge bugs
**Was:** Requiring two approvals on all PRs reduces post-merge bugs compared to one approval.
**Evidence against:** 40 PRs tracked over 6 weeks. Bug rate identical (7.5% vs 8%). Second reviewer rubber-stamped after seeing first approval.
**Replaced by:** `review-patterns.md` — require domain-expert approval for PRs touching specific subsystems, not a blanket second approval.
**Rejected:** 2026-03-01
