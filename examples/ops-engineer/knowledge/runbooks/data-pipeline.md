# Runbook: Data Pipeline

## Quick Diagnosis

1. Check consumer lag: `kafka-consumer-groups --describe --group main-consumer`
2. Check producer throughput: pipeline dashboard, "Events/sec" panel
3. Check for failed messages: `kafka-console-consumer --topic dead-letter-queue --from-beginning --max-messages 5`

## Common Scenarios

### Consumer lag increasing steadily
Likely: throughput exceeded consumer capacity. Scale consumers: `kubectl scale deploy pipeline-consumer --replicas=N`

### Consumer lag spike then recovery
Likely: temporary burst (marketing campaign, batch job). Monitor for 15 minutes before scaling.

### Messages in dead letter queue
Check message format. Common cause: schema change without consumer update. Fix consumer, then replay DLQ.

## Emergency: Full Pipeline Reset
Only if pipeline is corrupted beyond recovery:
1. Stop all consumers
2. Reset consumer group offset: `kafka-consumer-groups --reset-offsets --to-latest --execute --group main-consumer --all-topics`
3. Restart consumers
4. WARNING: This skips unprocessed messages. Document what was skipped.
