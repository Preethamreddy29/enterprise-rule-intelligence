# RuleTwin NFR Hypotheses

Targets are from the available handbook/runbook unless labeled otherwise. They are not measured and must be validated against a named local machine before a release claim.

| Concern | Initial target / constraint | Verification |
|---|---|---|
| Cost/deployment | ₹0 cash cost; local Docker Compose; no permanently hosted backend or managed services | Dependency/infrastructure inventory and clean local start |
| Isolation | No cross-tenant result; 100% complete isolation suite pass | Role/path/filter/export/artifact/worker/metrics matrix |
| Determinism | Same engine/rule/dataset/policy version tuple yields identical canonical checksum | Repeated golden runs across restart; evaluator report |
| Simulation scale | Design workload: 3 tenants and 100,000 events on reference laptop | Measured load profiles with hardware, dataset, version, resource use |
| Latency | Simulation acknowledgement P95 <750 ms hypothesis; define 10k completion target after baseline | Load test and separate queue/replay/request timing |
| Reliability | Acknowledged simulation not lost on worker crash; idempotent duplicate request | Crash-point integration suite with PostgreSQL/outbox |
| Audit | 100% protected-mutation audit completeness | Mutation-to-audit assertion and export inspection |
| Security | No arbitrary code execution; risk-policy failure closed; zero dangerous false-safe | Hostile inputs and fault-injected policy/evaluation corpus |
| Accessibility | Keyboard navigation, semantic forms, focus/error/contrast basics | Manual checklist plus automated/browser testing in Phase 4/7 |
| Operability | Liveness/readiness per service; structured redacted logs; correlation ID; RED/USE and worker metrics | Compose unhealthy dependency and telemetry smoke tests |
| Recovery | Handbook initial DB RPO 24h/RTO 60m, with design target RPO 15m; recover from tested backup | Scripted backup/restore into clean DB and timed recovery rehearsal |

Revise targets only with explicit evidence and ADR/PR context. A lower score cannot replace a hard safety/isolation gate.
