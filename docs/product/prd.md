# RuleTwin PRD-lite (v1 target)

## Goal

Make a proposed tenant-specific business-rule change reviewable through reproducible baseline-versus-candidate replay before release.

## Primary user story

As a release manager, I need a deterministic tenant/scenario impact report tied to exact rule, event-set, engine, and risk-policy versions, so I can approve, ask for revision, or block the proposal and later reproduce the decision.

## Critical workflow

Candidate rule → scope/dependency validation → reproducible dataset → async baseline/candidate replay → impact comparison → deterministic risk evaluation → human review/approval or block → immutable evidence.

## Functional requirements

| ID | Requirement | Acceptance outline |
|---|---|---|
| RT-F01 | Store immutable validated rule versions with tenant scope, effective time, dependency references, author, canonical form, and checksum. | Invalid schemas, incompatible dependencies, and prohibited executable input are rejected; stored versions cannot be silently changed. |
| RT-F02 | Generate deterministic synthetic replay datasets from seed and generator version. | Same seed/generator/config yields same manifest and canonical event checksums. |
| RT-F03 | Evaluate current and proposed rule versions in isolated deterministic contexts. | No arbitrary user-code execution; inputs and resource budgets are bounded. |
| RT-F04 | Compare amount, workflow state, error, emitted events, and measured execution duration. | Differences link to tenant/scenario/event and preserve exact input/output provenance. |
| RT-F05 | Aggregate effects by tenant, rule, scenario, and consequence; over-include when uncertain rather than silently omit possible impact. | API and UI label scope/coverage and do not imply tested behavior outside selected scenarios. |
| RT-F06 | Evaluate using immutable versioned risk policies with fail-closed defaults. | Missing/invalid/unavailable policy cannot produce a safe/allow result. Dangerous release fixtures never pass at release. |
| RT-F07 | Enforce tenant isolation, object authorization, role/action permissions, and author/reviewer/approver separation. | Server checks every access/mutation; negative-path matrix returns no cross-tenant data. |
| RT-F08 | Bind approval/release gate to exact simulation result checksum and risk-policy version. | Stale, substituted, incomplete, or self-authored evidence is rejected. |
| RT-F09 | Make acknowledged async runs idempotent, recoverable, and auditable. | Duplicate key returns same logical request; worker crash does not lose acknowledged work or duplicate final effects. |
| RT-F10 | Reproduce a prior outcome from exact engine, rule, dataset, and policy versions. | Identical version tuple yields identical canonical outcome checksum. |
| RT-F11 | Expose stable versioned API and machine-readable errors. | OpenAPI validates; mutation idempotency/correlation, status, pagination, concurrency, and errors follow contract. |
| RT-F12 | Provide an accessible role-aware web path and operational health/telemetry. | Loading/empty/partial/error/unauthorized states are explicit; API is authoritative for access. |

## v1 rule and scenario scope

Declarative families: rounding; tiered rate; late fee; effective-date eligibility; exception routing. The first complete vertical slice is narrower: one tenant, rounding, 100 deterministic synthetic events, baseline/candidate, impact, allow/block, author and approver. Later increments add multi-tenancy and five families.

Signature fixture design: three fictional tenant configurations share a system but differ in settings. A candidate rounding-policy revision is replayed on an identical versioned synthetic event cohort. Expected outcomes deliberately include a changed result for at least one tenant and no change for a control tenant. Exact event values and golden outputs will be committed with the executable evaluator in Phase 3/4 and reviewed before any performance/accuracy claim.

## Non-functional target hypotheses

- Initial workload design: 3 tenants and up to 100,000 events on a named reference laptop.
- Simulation request acknowledgement P95 below 750 ms (not measured; target hypothesis).
- Establish a measured completion target for 10,000 events after a baseline exists; do not invent one in advance.
- 100% same-tuple replay determinism, 0 dangerous false-safe outcomes, 100% isolation suite pass, and 100% audit coverage for protected mutations are hard release targets.
- No data loss for acknowledged simulations under worker failure; duplicate submission is idempotent.

These are targets, not achieved results. Hardware, dataset manifest, exact commit and test output must accompany measured claims.

## Out of scope

Production billing/payment mutation, invoice issuance, arbitrary code, AI rule authoring/approval, external customer integrations, DecisionTrace/BoundaryOps runtime, cloud deployment, and unbounded/unreviewed event uploads.

## UX and API outline

Planned v1 endpoints: create/get/diff rule versions; create replay dataset; create/get simulation and impact; submit approval; evaluate release gate; list audit events. Mutations use idempotency and correlation IDs; async simulation returns accepted status; stale concurrency returns conflict; domain validation returns typed validation response. Exact path schemas are Phase 1 deliverables and must be documented in OpenAPI before code.

## Success and guardrail measures

See [metrics](metrics.md). Product value measures do not override zero-unsafe-pass, isolation, audit, determinism, or fail-closed gates.
