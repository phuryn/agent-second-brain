# Example Hypothesis Entry

This file shows what a well-formed hypothesis looks like at each stage of its lifecycle. Do not use this for actual hypotheses — it's a reference only. When adding a real hypothesis, add it to `index.md`.

---

## Example: Active Hypothesis

### HYP-007
**Statement:** LinkedIn posts that include a specific failure story in the first 3 lines generate 2x+ comments compared to posts that open with a general observation.
**Status:** active
**Created:** 2026-02-14
**Platform/context:** LinkedIn long-form posts (800+ words), audience = product managers and operators

**Evidence for:**
- 2026-02-14 "The $2M mistake": opened with specific failure → 47 comments (baseline avg: 18)
- 2026-03-01 "Why my first PM role almost ended my career": specific failure opener → 63 comments

**Evidence against:**
- 2026-02-28 "The product launch that taught me everything": specific failure opener → 14 comments (below baseline)
  - Note: This was posted on a Sunday. May be confounding factor.

**Notes:** Need 1 more data point before graduation. Testing again on a Thursday post. If the Sunday post is excluded, 2/2 support. If included, 2/3 support with unclear confound.

---

## Example: Graduated Hypothesis

### HYP-003
**Statement:** Newsletter subject lines under 40 characters have higher open rates than subject lines over 60 characters for this audience.
**Status:** graduated
**Graduated:** 2026-01-20
**Now lives in:** `platforms/newsletter/rules.md` as Rule: "Subject lines: 30-40 characters maximum"

**Evidence summary:** 5 A/B tests over 8 weeks. Under-40-char subjects averaged 34% open rate; over-60 averaged 27%. One exception (a 55-char subject on a major announcement hit 38%) — noted as context-dependent and excluded from rule scope.

---

## Example: Rejected Hypothesis

### HYP-011
**Statement:** Ending LinkedIn posts with a direct question increases comments by 50%+.
**Status:** rejected
**Rejected:** 2026-03-15
**Reason:** Tested in 7 posts over 6 weeks. 4 performed at or below baseline despite ending questions. 2 performed above baseline — but both had unusually strong content; a different ending wouldn't have changed outcome. Direct questions may increase low-quality comments but don't reliably increase meaningful engagement.

**Notable finding:** Posts ending with a question generated more one-word "yes/no" replies. This inflated comment count in platform metrics but didn't increase meaningful engagement (saves, follows, DMs).

**See also:** `platforms/linkedin/false-beliefs.md` — "Belief: Ending with a question boosts engagement"
