# Code Review Patterns

Rules for reviewing pull requests. Evidence-backed — each rule graduated from a hypothesis.

---

## Rules

### R1 — Flag dependency changes that cross service boundaries
When a PR modifies a shared library or proto definition, flag it for cross-team review even if tests pass. Three incidents in 2025 traced to uncoordinated dependency bumps.

### R2 — Prefer explicit error types over generic error wrapping
Generic `fmt.Errorf("failed: %w", err)` hides the original error type from callers. Use typed errors for any error that crosses a package boundary. Graduated from HYP-004 (5 data points: debugging sessions where wrapped errors added 30+ min).

### R3 — Max 3 review comments per file unless systemic
More than 3 per file signals the PR is too large or the pattern is systemic. If systemic, leave one comment linking to the pattern and request a follow-up PR.
