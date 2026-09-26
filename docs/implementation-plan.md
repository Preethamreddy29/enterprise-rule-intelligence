# Portfolio Implementation Plan and Gates

This plan follows the handbook and product-specific runbooks. It is staged, not a promise of completion dates. Work stops or scope narrows when an exit gate fails. At present only portfolio/RuleTwin Phase 0 documentation is in scope.

## Portfolio dependency sequence

1. Portfolio engineering foundation and RuleTwin Phase 0–1.
2. RuleTwin Phase 2–9 through tagged local production v1.
3. DecisionTrace Phase 0–9 only after RuleTwin v1; no work started now.
4. BoundaryOps product discovery may be planned later, but runtime implementation waits for tagged RuleTwin and DecisionTrace v1 contracts, example fixtures, and passing mock consumer contract tests.
5. Integrated release/demo/evidence only after each product independently satisfies its gates.

## Phases 0–9

| Phase | Deliverables | Dependencies | Tests/evidence | Completion / decision gate |
|---:|---|---|---|---|
| 0 — Charter (content gate satisfied) | RuleTwin charter, problem brief, current/future journey, PRD-lite, metrics, risk register, synthetic scenario/notice, traceability, initial architecture/threat model and ADRs | Handbook/runbook/evidence matrix/blueprint reviewed; portfolio-index role confirmed | Phase 0 audit, evidence labels, assumptions with falsification methods; no runtime tests claimed | Specific user/problem, critical workflow, non-goals, synthetic three-tenant scenario, measurable metrics and at least 3 testable assumptions. Worth building? **Satisfied in documentation; Git baseline still awaits approval.** |
| 1 — Requirements/architecture | Domain/data/API specifications, eight RuleTwin ADRs, NFR baselines, ERD, OpenAPI, threat-to-test mapping, policy and tenant model | Phase 0; repository topology and license decision | Schema/OpenAPI validation; threat review; traceability coverage | Safe/feasible design, high risks have controls/tests, all critical requirements traceable. |
| 2 — Engineering foundation | Confirm RuleTwin repo; CI/tooling; Compose core stack; health/readiness; PostgreSQL migration/roles/seeds; request IDs/logging; worker/outbox skeleton; minimal readiness UI | Phase 1 contracts and approved repo boundary; local Docker/Python/Node | clean migration, DB up/down/forward policy, unhealthy readiness, error mapping, worker claims safely, non-root container, planted-secret scanner test | One documented command starts core; one runs checks; CI clean build; evidence recorded. No product claim. |
| 3 — Vertical slice | One tenant, rounding, 100 deterministic events, baseline/candidate, impact, risk block/allow, author/approver, UI, audit | Phase 2; schema and API ready | canonicalization/property tests, idempotency, crash recovery, deterministic checksum, stale/self approval rejection, Playwright critical flow | End-to-end evidence path reproducible without manual DB edits. |
| 4 — MVP | Multi-tenant RBAC; five rule families; dependency/cycle handling; three tenants; impact dimensions; risk versions; approvals; mock webhook; auditor reproduction/export; usable UI | Phase 3 and accepted UX/security boundaries | complete role/action matrix; cross-tenant every path; dates/timezones; pagination/export; duplicate/invalid webhook | All v1 functional requirements work; no critical authorization gap; usability issues recorded. |
| 5 — Security/failure hardening | Resource budgets; rule interpreter constraints; approval evidence binding; artifact reauthorization; redaction; audit integrity controls; backup security design | Phase 4 | API/worker/DB/artifact/risk/webhook failure drills; hostile rules; isolation; redaction | Unsafe failures controlled, isolation suite passes, failures visible; no false success. |
| 6 — Evaluation/observability | 40+ controlled fixtures; dashboard/metrics; load profiles; P50/P95 and throughput evidence; fairness decision from measurements | Phase 5; stable scenarios and instrumentation | dangerous false-safe 0; recall target >=.98; determinism/isolation/audit 100%; performance on named hardware | Versioned report meets hard gates; limitations and scale boundary documented. |
| 7 — Release candidate operations | Freeze API; migration/backup/restore, runbooks, recovery and rollback rehearsal; accessibility/browser/clean-machine validation; SBOM/scans | Phase 6; stable candidate | migration from prior tag; clean restore; stuck-job recovery; timed rollback; exact RC checks | Handbook release checklist passes; no unaccepted S0/S1/S2; restore/rollback proven. |
| 8 — Local production v1 | Promote exact RC images/digests; migrate with backup; synthetic signature smoke; dashboards/audit checks; tag dataset/eval | Phase 7 passed | exact release smoke and checksum; failure/rollback triggers checked | `v1.0.0` local production; only claims measured and evidenced. |
| 9 — Portfolio proof | README/demo/case study/economics/roadmap/defense answers; three product narrative sequenced as completed | RuleTwin release; later products only when independently done | 60-second/5-minute/30-minute defense; clean clone; release evidence review | Portfolio evidence is understandable and limitations explicit; no unsupported claims. |

## Active scope and deferred tasks

**Now:** review and merge the Phase 0 documentation PR, then begin Phase 1 design. **Phase 1:** create RuleTwin-owned domain/data/API specifications, eight ADRs, ERD, OpenAPI, threat-to-test mapping, and policy/tenant models; these may be drafted in the portfolio only as planning inputs, while authoritative product artifacts must live in the separate RuleTwin repository. **Before Phase 2:** choose a license, establish the RuleTwin repository, and resolve domain semantics. **Not now:** RuleTwin runtime, DecisionTrace implementation, BoundaryOps runtime, Docker/dependency installation, or CI/runtime scaffolding.

## Delivery and review method

Use short-lived feature branches, focused milestones, conventional commits only after a verifiable baseline exists, and no commit/push/PR without explicit approval. For each milestone record changed paths, exact commands/output, test results, assumptions, risks, and next gate in `docs/progress.md`. The proposed initial baseline and feature-branch sequence is recorded there; this turn does not execute it.
