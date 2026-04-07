# Architecture Decisions

Living record of architecture rules and their rationale. Each entry was either an explicit team decision or graduated from a tested hypothesis.

---

## Active Decisions

### AD-01 — All inter-service communication goes through the API gateway
No direct service-to-service calls. Exception: async events via the message bus.
**Rationale:** Direct calls created a hidden dependency graph that caused cascading failures in the 2025-06 outage.

### AD-02 — Database migrations must be backward-compatible for one release cycle
Every migration must work with both the current and previous version of the service code. Drop columns only after the next release confirms no rollback is needed.
**Rationale:** Graduated from HYP-002. Three rollback failures in Q3 2025 traced to non-backward-compatible migrations.

### AD-03 — Circuit breakers on all external API calls
Use a 5-second timeout with exponential backoff. No exceptions, even for "fast" external services.
**Rationale:** Team decision after the payment provider outage took down checkout for 45 minutes.
