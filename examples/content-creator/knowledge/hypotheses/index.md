# Hypothesis Index — Content Creator Example

**Active hypotheses:** 3
**Last reviewed:** 2026-04-01

---

## Active Hypotheses

### HYP-001
**Statement:** LinkedIn posts that open with a specific number (count, percentage, or dollar amount) generate 30%+ more comments than posts that open with a general observation.
**Status:** active
**Created:** 2026-02-01
**Platform/context:** LinkedIn long-form (600+ words), audience = product managers

**Evidence for:**
- 2026-02-14 "47 roadmaps, same problem" (opened with "47"): 89 comments vs. 18 baseline
- 2026-03-05 "After 3 years and $2M in wasted sprint work" (opened with numbers): 61 comments
- 2026-03-20 "12 PM interviews, 0 useful findings" (specific number opener): 44 comments

**Evidence against:**
- 2026-02-28 "5 signs your roadmap is a wish list" (numbered list opener): 22 comments — above baseline but not 30%+ threshold

**Notes:** 3 supporting data points, 1 weak counter. The Feb 28 post was published Sunday (confound). Strong enough to surface for graduation. Debate: is the effect from the number itself, or from the specificity the number implies? Testing with specific-but-non-numeric openers to isolate.

---

### HYP-002
**Statement:** Newsletter issues sent Tuesday 8am EST outperform Thursday 8am EST by 5%+ open rate for this audience, regardless of content quality.
**Status:** active
**Created:** 2026-01-15
**Platform/context:** Newsletter (4,200 subscribers, primarily US-based PMs and operators)

**Evidence for:**
- 2026-01-20 (Tue) vs. equivalent issue 2026-01-27 (Thu): 46% vs. 39% open rate
- 2026-02-04 (Tue) vs. 2026-02-11 (Thu): 51% vs. 44% open rate

**Evidence against:**
- 2026-03-03 (Tue): 38% open rate — below multiple Thursday issues (though this issue had a weaker subject line)

**Notes:** 2 clean supporting points, 1 counter with a confound. Need 1 more clean comparison. Planning a subject-line-matched A/B test in April.

---

### HYP-003
**Statement:** LinkedIn posts that include a specific decision framework (named, with clear criteria) generate 2x+ saves compared to posts that share insight without a reusable structure.
**Status:** active
**Created:** 2026-03-01
**Platform/context:** LinkedIn, all formats

**Evidence for:**
- 2026-03-10 "The 3-column prioritization test" (clear named framework): 340 saves vs. 80 baseline
- 2026-03-25 "How I decide what to cut from a roadmap" (framework with criteria): 280 saves

**Evidence against:**
- none yet

**Notes:** Early data is strong. Only 2 data points. Testing in April with 2 more framework posts. If this holds, it has implications for template design — frameworks should be named and reusable.

---

## Graduated Hypotheses

### HYP-G01 (formerly HYP-004)
**Statement:** Posts ending with a direct question ("What's your experience with X?") increase comments by 50%+.
**Status:** graduated — REJECTED (became a false belief)
**Decided:** 2026-02-01
**Outcome:** Hypothesis rejected. Data over 7 posts showed questions increase comment count, but mostly low-quality one-word replies. Meaningful comments (3+ sentences) did not increase. See `platforms/linkedin/false-beliefs.md`.

---

## Schema Reference

```markdown
### HYP-[NEXT NUMBER]
**Statement:** [Precise, testable, falsifiable claim]
**Status:** active
**Created:** [DATE]
**Platform/context:** [Where/when this applies]

**Evidence for:**
- [none yet]
**Evidence against:**
- [none yet]
**Notes:** [Testing plan or observations]
```
