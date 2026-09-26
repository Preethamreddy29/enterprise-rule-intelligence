# RuleTwin Risk Register (Initial Phase 0)

Likelihood/impact are qualitative hypotheses, not measured. “Open” means mitigation/evidence remains outstanding.

| ID | Risk | L/I | Planned control and verification | Owner | State |
|---|---|---|---|---|---|
| RR-01 | Tenant context omitted or confused; cross-tenant disclosure | M/H | Server-derived identity scope; tenant-scoped repositories and DB constraints; adversarial API/export/worker isolation suite. | Product implementation | Open; release blocker |
| RR-02 | Rule input executes arbitrary code or causes resource exhaustion | M/H | Strict declarative JSON Schema, allowlisted interpreter, depth/size/operator/event/time budgets; hostile-input tests. | Domain/API/worker | Open; release blocker |
| RR-03 | Candidate produces harmful change but policy reports safe | M/H | Deterministic comparison; dangerous golden set; fail-closed policy; false-safe rate must be 0. | Domain/policy | Open; release blocker |
| RR-04 | Approval is replayed, self-approved, or bound to substituted result | M/H | Separation of duties; exact result/policy checksum binding; expiry and concurrency checks; negative-path tests. | API/domain | Open; release blocker |
| RR-05 | Dataset, rule, or result changes after decision; reproduction fails | M/H | Immutable versioned records, canonical checksum, retention contract; repeat-run/restart tests. | Data/domain | Open |
| RR-06 | Worker/API crash after acknowledgment loses or duplicates run | M/H | Transactional outbox, idempotency, lease/heartbeat and dedup; crash-point integration tests. | Worker/data | Open |
| RR-07 | Financial precision/date semantics differ from expectations | M/H | Decide integer minor units vs exact decimal and timezone/effective-date semantics in Phase 1; property and boundary tests. | Product/domain | Open |
| RR-08 | Synthetic fixtures are mistaken for representative customer evidence | M/M | Label every fixture synthetic; synthetic-data notice; disclose scope and evaluation limitations in reports. | Docs/product | Mitigation documented; monitor |
| RR-09 | Logs, exports, metrics, or artifacts expose tenant-sensitive information | M/H | Minimize/redact; reauthorize artifact reads; bound export; scan logs/metrics/artifact paths in isolation suite. | API/ops | Open |
| RR-10 | Runtime or product-owned contracts are accidentally added to the portfolio index | M/M | ADR-001 fixes this checkout as portfolio index; repository layout and phase reviews prohibit runtime here; create a separate RuleTwin repository before Phase 2. | Maintainer | Topology resolved; boundary monitored |
| RR-11 | Local resource limits or unpaid infrastructure constraint prevent target throughput | M/M | Local Compose only, measure on named hardware, make profile opt-in, report measured vs estimated scale. | Maintainer/ops | Open |
| RR-12 | Audit records mutable/deletable by application identity | L/H | Append-only application access, DB privileges/checks, hash/digest experiment with documented limitations; mutation tests. | Data/security | Open |

Review on each phase transition and whenever a data flow, authorization boundary, or action changes.
