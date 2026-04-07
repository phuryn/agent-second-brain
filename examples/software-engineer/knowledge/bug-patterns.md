# Bug Patterns

Recurring bug categories in this codebase. Load during bug investigation to check if the current bug matches a known pattern.

---

## Patterns

### BP-01 — Race condition in cache invalidation
**Signal:** Stale data appears intermittently under load, disappears on retry.
**Root cause:** Cache invalidation message arrives before the write is committed to the primary DB.
**Fix pattern:** Read-after-write consistency check, or invalidate with a delay equal to replication lag.
**Occurrences:** 3 (auth service, product catalog, session store)

### BP-02 — Silent truncation in batch processing
**Signal:** Batch job reports success but output is incomplete. No errors in logs.
**Root cause:** Upstream API returns paginated results; batch processor only reads first page.
**Fix pattern:** Always check for pagination tokens. Add assertion: output count >= expected count.
**Occurrences:** 2 (data export, report generator)
