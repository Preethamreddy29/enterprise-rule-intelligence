# RuleTwin Initial Threat Model (Phase 0)

## Status and scope

Initial design-only model; no running application exists. This is not a completed STRIDE assessment or proof of controls. Threats are reviewed at Phase 1 architecture and before each release. Assets: tenant data, rule versions, dataset/event inputs, simulation results, approvals, release gates, audit history, credentials, and availability.

## Trust boundaries / data flows

See [system context](../architecture/portfolio-boundaries.md). Browser/API, API/worker, worker/PostgreSQL, artifact storage, tenant-to-tenant access, and any later upstream contract are separate trust boundaries. Rule/event input and generated artifacts are untrusted. Identity/tenant scope comes from server-authenticated context, never from an untrusted payload alone.

## STRIDE and safety risks

| Threat | Category | Impact | Planned prevention/detection | Release evidence |
|---|---|---|---|---|
| Tenant A accesses Tenant B result through ID, filter, export, artifact or worker | Spoofing / Information disclosure | S0 cross-tenant leak | Server-derived tenant scope; object authorization; composite constraints/indexes; consider DB RLS as defense in depth. | Full negative tenant matrix across API, UI, worker, exports, metrics and artifacts; zero leakage. |
| Rule payload invokes code or creates pathological computation | Tampering / DoS | S0 unsafe code or service exhaustion | Strict declarative schema, allowlisted interpreter, nesting/operators/input/event/time budgets; no eval/exec. | Hostile JSON, deep nesting, unknown operators, boundary and budget tests. |
| Dataset or rule is substituted after simulation/approval | Tampering / Repudiation | Unsafe release decision | Immutable versions, canonical checksums, exact tuple binding, append-only audit. | Mutation/substitution/stale approval rejection; reproducible checksum. |
| Reviewer self-approves or approval is replayed | Elevation of privilege / Tampering | Unreviewed risky change | Server RBAC, separation of duties, approval expiry/nonce/concurrency and evidence checksum binding. | Full authorization and replay negative tests. |
| Risk policy missing, invalid, or unavailable results in allow | Elevation / Fail-open | Dangerous false-safe | Deterministic fail-closed evaluator with stable reason codes. | Fault-injection test demonstrates deny/block, never allow. |
| Worker/API crash after acknowledgment loses/duplicates simulation | Denial of service / Tampering | Lost or inconsistent evidence | Transactional outbox, idempotency, leases, deduplication and explicit state machine. | Crash at every transaction/side-effect boundary; no lost acknowledged work or duplicate final result. |
| Audit records are altered/deleted or logs omit protected changes | Repudiation / Tampering | Cannot defend decision | Least-privilege DB grants, append-only application behavior, audit completeness checks and log redaction. | Mutation permission tests, audit coverage report, redaction checks; document hash-chain limits. |
| Oversized events, exports, or simulations exhaust local resources | DoS | Unavailable service/noisy tenant | Request/result limits, per-tenant budgets/concurrency, bounded artifact and retention design. | Load, oversized payload and noisy-neighbor drills. |
| Logs/metrics/artifacts expose identifiers or sensitive tenant outcomes | Information disclosure | Privacy/trust loss | Minimize and pseudonymize; redact; authorize downloads; limit labels/exports; synthetic-only fixtures. | Log/metric/artifact inspection and cross-tenant negative tests. |
| Effective dates, money precision, or timezone are ambiguous | Tampering / integrity | Incorrect outcome without obvious failure | Explicit Phase 1 semantics, exact arithmetic, UTC normalization, golden boundary tests. | Leap/day/timezone and rounding property tests; reviewed ADR. |
| Dependency/contract drift produces untrusted or incompatible results | Tampering / DoS | Misleading release evidence | Pin/validate schemas; timeout/circuit limits; no live integration for current RuleTwin scope. | OpenAPI/schema compatibility and dependency failure tests. |
| Synthetic fixture mistaken for empirical customer evidence | Information disclosure / trust | Misleading portfolio claims | Prominent labels, no real data ingestion, evidence provenance. | Review README, reports, and demo labels before release. |

## Security requirements and unknowns

- Define authentication/token lifecycle and local OIDC evolution in Phase 1; no identity implementation exists.
- Strictly validate inputs and reject unknown dangerous fields; parameterized SQL only.
- Bound pagination/body/result size and expensive simulation rate by actor and tenant.
- Use idempotency keys, optimistic concurrency, stable machine-readable errors, correlation IDs, and redacted structured logs.
- Decide retention, artifact access, audit immutability, encryption at rest/backup, and safe export behavior before relevant implementation.
- Threat-model file ingestion only if introduced; local MVP should prefer generated fixtures and avoid arbitrary uploads.

## Residual risk

Synthetic scenarios cannot establish customer impact, representativeness, scale, or security of a production billing environment. Until real tests exist, every control is planned, not verified. Any cross-tenant leak, unsafe arbitrary execution, dangerous false-safe, or missing audit evidence is a release blocker.
