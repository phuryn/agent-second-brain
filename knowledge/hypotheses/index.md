# Hypothesis Index

This is the system's learning layer. Hypotheses are things you're testing — not yet rules, but not random guesses either. They should be specific enough to confirm or deny.

---

## How This Works

**Hypothesis → Rule** (graduation): When a hypothesis has 3+ data points supporting it and 0 strong counter-examples, surface it for graduation. If confirmed, move the insight to the relevant knowledge file as a rule.

**Hypothesis → Rejected** (rejection): When a hypothesis has 2+ data points against it, or 0 supporting data points after 8+ tests, mark it rejected. Move to an `archive/` file if the counter-evidence is worth keeping.

**Active**: Currently being tested. Don't enforce as a rule yet.

**On hold**: Paused — not enough data yet and no active way to test it.

---

## Graduation Criteria

A hypothesis graduates when:
- 3 or more distinct data points support it
- At least 1 data point comes from a situation the hypothesis was not designed for (generalization)
- No strong counter-example exists in the same context

Graduation process:
1. Note the hypothesis ID and data points
2. Decide which knowledge file it belongs in
3. Write the rule with the evidence summary
4. Mark hypothesis as "graduated" here
5. Update INDEX.md if the rule changes routing

---

## Rejection Criteria

A hypothesis is rejected when:
- 2+ data points directly contradict it
- OR: it's been active for 90+ days with zero supporting data points
- OR: the conditions under which it would be testable no longer exist

Rejection process:
1. Mark as "rejected" here
2. Move to `rejected.md` with the evidence that killed it
3. If the rejection is surprising, note why in the entry

---

## Active Hypotheses

### HYP-001
**Statement:** [Precise, testable claim — specific enough that you can describe what would prove it wrong]
**Status:** active
**Created:** [DATE]
**Context:** [Where/when this applies]
**Evidence for:**
- [none yet]
**Evidence against:**
- [none yet]
**Notes:** [How you'll test this, or initial observations]

---

## Graduated Hypotheses

*(Hypotheses that became rules. Kept here as one-line stubs for traceability. Full evidence moves to the target knowledge file. Archive stubs older than 6 months to `hypotheses/archive.md` — see `system-maintenance.md`.)*

### HYP-[N]
**Statement:** [Original hypothesis]
**Status:** graduated
**Graduated:** [DATE]
**Now lives in:** `knowledge/[file].md` as Rule [X]
**Evidence summary:** [N data points supporting, N against]

---

## Rejected Hypotheses

*(Hypotheses that were tested and failed. Kept here as institutional memory.)*

### HYP-[N]
**Statement:** [Original hypothesis]
**Status:** rejected
**Rejected:** [DATE]
**Reason:** [Why it was rejected — data points, changed context, etc.]
**Notable finding:** [Anything interesting from the failure]

---

## Schema Reference

When adding a new hypothesis, use this format:

```markdown
### HYP-[NEXT NUMBER]
**Statement:** [Precise, testable claim. Should be falsifiable.]
**Status:** active
**Created:** [DATE]
**Context:** [Where/when this applies]
**Evidence for:**
- [none yet]
**Evidence against:**
- [none yet]
**Notes:** [How you'll test this, or initial observations]
```

Rules for writing a good hypothesis:
- Must be falsifiable: you can describe what would prove it wrong
- Must be specific: includes a context, a claim, and (ideally) a measurable signal
- Must be distinct: not a restatement of an existing rule
