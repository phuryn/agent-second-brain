# Incident Patterns

Recurring incident categories across the platform. Load during active incidents to check if the current incident matches a known pattern.

---

## Patterns

### IP-01 — Cascading timeout from external dependency
**Signal:** Error rate spikes across multiple services simultaneously. Latency increases before errors.
**Root cause:** An external dependency slows down, consuming connection pool threads. Services queue up, timeouts cascade.
**Mitigation:** Circuit breaker activation. Verify circuit breaker thresholds in `runbooks/api-gateway.md`.
**Occurrences:** 4 (payment provider 2x, geolocation API, email service)

### IP-02 — Data pipeline backpressure causing stale reads
**Signal:** Dashboard shows data that's hours old. No errors in pipeline logs — just lag.
**Root cause:** Upstream event volume exceeds consumer throughput. Consumer falls behind without failing.
**Mitigation:** Scale consumers, or enable backpressure signaling to producers. See `runbooks/data-pipeline.md`.
**Occurrences:** 3 (Black Friday 2025, marketing campaign spike, schema migration replay)

### IP-03 — Auth token refresh storm after deploy
**Signal:** Auth service CPU spikes to 100% within 5 minutes of deploy. All other services report auth failures.
**Root cause:** Deploy invalidates cached tokens. All clients refresh simultaneously.
**Mitigation:** Staggered token expiry. See `runbooks/auth-service.md`.
**Occurrences:** 2 (2025-09, 2025-12)
