# Runbook: Auth Service

## Quick Diagnosis

1. Check CPU and memory: Grafana `auth-service` board
2. Check token refresh rate: if >200/sec, likely a refresh storm
3. Check recent deploys: `kubectl rollout history deploy/auth-service`

## Common Scenarios

### CPU spike after deploy (token refresh storm)
See incident pattern IP-03. Mitigation: wait 10 minutes for storm to subside. If service is unhealthy, scale horizontally first, then investigate.

### Intermittent auth failures
Check token cache hit rate. If below 80%, cache may be undersized or tokens are expiring too fast. Adjust TTL in config.

### Complete auth outage
1. Check database connectivity (auth service depends on user DB)
2. Check if SSL certificates have expired
3. Failover to backup auth service: update API gateway routing

## Rollback Procedure
1. `kubectl rollout undo deploy/auth-service`
2. Monitor token refresh rate — should return to baseline within 5 minutes
3. If refresh storm persists after rollback, restart all client services in rolling fashion
