# Draft Gate

A quality gate is not a style guide. It's a binary pass/fail system. Run this before any output is published or sent. There are two stages: quick scan and full gate. Don't run the full gate if the quick scan fails.

---

## Stage 1: Quick Scan (Run First)

These are instant killers. If any of these are true, stop and fix before proceeding.

**Structural killers:**
- [ ] The piece has no clear single point (reader couldn't summarize it in one sentence)
- [ ] The opening does not earn attention in the first 2 sentences
- [ ] The piece ends without a landing — it just stops

**Content killers:**
- [ ] A claim is made without evidence, example, or mechanism
- [ ] The piece contradicts a hard rule in the platform's `rules.md`
- [ ] The piece relies on a hypothesis that is not flagged as such

**Relevance killers:**
- [ ] This exact topic/angle was covered in the last 30 days (check `posts/db_YYYYMM.csv`)
- [ ] The piece is about the writer's process, not the reader's problem

If all quick-scan items pass: proceed to full gate.
If any fail: fix the issue, then re-run quick scan before proceeding.

---

## Stage 2: Full Quality Gate

Run this only after Stage 1 passes.

**Clarity:**
- [ ] Every sentence is necessary — no sentence could be cut without losing meaning
- [ ] No jargon that the target audience wouldn't recognize immediately
- [ ] The core insight is stated explicitly, not just implied

**Specificity:**
- [ ] At least one concrete example, number, or named instance per major point
- [ ] No vague qualifiers ("many," "often," "some people") without backing
- [ ] If a comparison is made, both sides are specific

**Structure:**
- [ ] Subheadings (if used) are informative, not decorative — they carry meaning
- [ ] The pacing matches the platform's reading context (skimmable vs. deep read)
- [ ] The strongest point is not buried in the middle

**Voice:**
- [ ] The piece sounds like the defined voice — not generic AI prose
- [ ] No throat-clearing phrases ("In this article, I will explain...")
- [ ] Contractions and sentence variety match the voice profile

**Platform fit:**
- [ ] Length is within the platform's benchmark range
- [ ] Format matches platform norms (paragraphs vs. bullets vs. threads)
- [ ] Call to action (if any) matches what's allowed on this platform

**Final check:**
- [ ] Read the first and last sentence only — does the piece earn its ending?
- [ ] Would a reader who finishes this feel they got something they didn't have before?

---

## Gate Result

**Pass:** All Stage 2 items checked. Output is ready.

**Conditional pass:** 1-2 items are "close enough" and deviation is intentional. Note which items and why.

**Fail:** Fix the failing items. Do not publish. Re-run Stage 1 before re-running Stage 2.

---

## Notes

The gate is not about perfection. It's about preventing the specific failure modes that are hardest to see when you're close to the work. A piece can have rough edges and still pass. A piece with a missing core point always fails.

When in doubt, ask: "What is this piece for? Did it do that?"
