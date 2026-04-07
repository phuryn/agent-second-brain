# Methodology Notes

Rules and patterns for experiment design in this lab. Each rule either reflects a team decision or graduated from a tested hypothesis.

---

## Rules

### M1 — Minimum run time: 7 days for behavioral metrics
Short runs (under 72 hours) produce high-variance results for this user cohort. Graduated from HYP-003 (5 experiments: sub-72h averaged +/-18% variance vs +/-6% for 7d+ runs).

### M2 — Always validate static structure predictions with short MD runs
15% of static predictions diverge significantly from MD equilibrium. A 10ns MD run catches most of these. Based on Chen & Park (2024) framework and 3 internal validations.

### M3 — Report confidence intervals, not just point estimates
Lab policy after two grant reviewers flagged missing uncertainty quantification. Applies to all computational results in papers and presentations.

---

## Common Methodology Pitfalls

### P1 — Overfitting to training distribution
**Signal:** Model performs well on benchmark but poorly on novel protein families.
**Mitigation:** Hold out entire protein families, not just individual structures. Cross-validate at the family level.

### P2 — Ignoring equilibration in MD runs
**Signal:** Energy drift in first 2ns of simulation.
**Mitigation:** Discard first 20% of trajectory as equilibration. Monitor RMSD convergence before analysis.
