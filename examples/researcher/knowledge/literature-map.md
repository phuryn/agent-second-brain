# Literature Map

Key papers and their relationships for the current research focus. Load when synthesizing literature or checking if a finding has prior art.

---

## Core Papers

### AlphaFold2 (Jumper et al., 2021)
- Attention-based architecture for protein structure prediction
- Key insight: MSA processing + structure module with iterative refinement
- Limitation: static prediction, no dynamics
- **Connects to:** ESMFold (language model alternative to MSA), MD validation studies

### ESMFold (Lin et al., 2023)
- Single-sequence structure prediction using protein language models
- Key insight: Competitive accuracy without MSA, 60x faster inference
- Limitation: Lower accuracy on orphan proteins with no evolutionary signal
- **Connects to:** AlphaFold2 (benchmark comparison), our HYP-001 (speed vs accuracy tradeoff)

### Molecular Dynamics Validation Framework (Chen & Park, 2024)
- Framework for validating static predictions against MD trajectories
- Key insight: 15% of AlphaFold2 predictions diverge significantly from MD equilibrium structures
- **Connects to:** Our methodology-notes.md Rule M2 (always validate static predictions with short MD runs)

---

## Research Gaps

- No systematic study of when single-sequence models outperform MSA-based models for disordered regions
- Limited work on transfer learning between protein families for dynamics prediction
- Confidence calibration for structure prediction models remains poorly characterized
