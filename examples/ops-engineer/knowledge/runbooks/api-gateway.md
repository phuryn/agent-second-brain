# Runbook: API Gateway

## Quick Diagnosis

1. Check error rate on Grafana `api-latency` board
2. Check if circuit breakers are tripped: `kubectl get cm circuit-breaker-status -o yaml`
3. Check upstream dependency health: `curl -s internal-healthcheck/dependencies | jq .`

## Common Scenarios

### High latency, no errors
Likely: upstream dependency slowdown. Check circuit breaker thresholds. If approaching trip threshold, manually trip to fail fast.

### Error spike, all endpoints
Likely: auth service issue. Check auth service health first. See `runbooks/auth-service.md`.

### Error spike, single endpoint
Likely: downstream service issue specific to that endpoint. Check that service's health directly.

## Rollback Procedure
1. Identify current version: `kubectl get deploy api-gateway -o jsonpath='{.spec.template.spec.containers[0].image}'`
2. Roll back: `kubectl rollout undo deploy/api-gateway`
3. Verify: watch error rate for 5 minutes post-rollback
