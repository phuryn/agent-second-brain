# Hypothesis Index

---

## Active Hypotheses

### HYP-001
**Statement:** Single-sequence models (ESMFold) outperform MSA-based models (AlphaFold2) for intrinsically disordered regions longer than 30 residues.
**Status:** active
**Created:** 2026-02-15
**Context:** Human proteome, disorder predictions validated against NMR ensembles
**Evidence for:**
- 2026-02-15 IDR benchmark: ESMFold RMSD 2.1A vs AlphaFold2 3.8A on 12 disordered regions
- 2026-03-01 Tau protein: ESMFold captured known conformational ensemble better
**Evidence against:**
- [none yet]
**Notes:** Need to test on non-human proteins. Current data is human-proteome biased.

### HYP-004
**Statement:** Adding solvent-accessible surface area (SASA) as an auxiliary training objective improves binding site prediction accuracy by >10%.
**Status:** active
**Created:** 2026-03-05
**Context:** Fine-tuning ESMFold for binding site prediction
**Evidence for:**
- 2026-03-05 Pilot run: +8% accuracy on test set (borderline, need more data)
**Evidence against:**
- [none yet]
**Notes:** Running larger-scale experiment. Results expected by 2026-03-20.

---

## Graduated Hypotheses

### HYP-003
**Statement:** Experiment run times under 72 hours produce higher variance results than runs over 7 days for this user cohort.
**Status:** graduated
**Graduated:** 2026-01-20
**Now lives in:** `knowledge/methodology-notes.md` as Rule M1
**Evidence summary:** 5 experiments over 10 weeks. Sub-72h averaged +/-18% variance; 7d+ averaged +/-6%.

---

## Rejected Hypotheses

### HYP-002
**Statement:** Pre-training on bacterial protein structures improves prediction accuracy for human membrane proteins.
**Status:** rejected
**Rejected:** 2026-02-28
**Reason:** 4 experiments showed no improvement. Bacterial membrane protein topology differs enough that transfer learning adds noise rather than signal.
**Notable finding:** Transfer learning works within the same kingdom (human-to-human) but not across (bacteria-to-human) for membrane proteins specifically. Worth testing for soluble proteins separately.
