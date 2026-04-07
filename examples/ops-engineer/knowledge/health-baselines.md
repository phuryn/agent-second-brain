# Health Baselines

Normal operating ranges for key platform metrics. Load during capacity planning or when investigating anomalies.

---

## Service Baselines

| Service | Metric | Normal range | Alert threshold | Source |
|---------|--------|-------------|-----------------|--------|
| API Gateway | p99 latency | 80-120ms | >200ms | Grafana api-latency board |
| API Gateway | Error rate | 0.1-0.3% | >1% | PagerDuty alert config |
| Auth Service | Token refresh rate | 50-80/sec | >200/sec | Custom metric |
| Data Pipeline | Consumer lag | 0-30 sec | >5 min | Kafka consumer group monitor |
| Data Pipeline | Throughput | 10K-15K events/sec | <5K events/sec | Pipeline dashboard |

---

## Seasonal Patterns

- **Monday 9am UTC:** 40% traffic spike (week start). Normal.
- **End of month:** 20% increase in payment-related API calls. Normal.
- **Black Friday/Cyber Monday:** 3-5x normal traffic. Pre-scale 48 hours ahead.

---

## Capacity Rules

### C1 — Scale triggers
Auto-scale when CPU exceeds 70% for 3 consecutive minutes. Graduated from HYP-001 (tested 60%, 70%, 80% thresholds; 70% balanced cost vs response time).

### C2 — Never scale down during business hours
Scale-down events during peak hours caused 2 incidents in 2025. Scale down only between 02:00-06:00 UTC.
