# Release Evidence Index — Initial Status

The authoritative thresholds and rows are in [the release evidence matrix](../04_RELEASE_EVIDENCE_MATRIX.md). This index maps those requirements to intended evidence. It does **not** mark any release gate as passed. Current repository has no runtime or test suite.

| Matrix area | Planned evidence location | Current state |
|---|---|---|
| Product / problem | `docs/product/charter.md`, `problem-brief.md`, journeys, PRD | Phase 0 documentation gate satisfied; role research is simulated only |
| Requirements traceability | `docs/requirements-traceability.md` | Initial mapping; planned paths/tests not implemented |
| Architecture | `docs/architecture/portfolio-boundaries.md`, repository layout | Target design only; portfolio-index boundary accepted; product architecture pending |
| Decisions (minimum five material ADRs) | `docs/decisions/` | Two Phase 0 ADRs (one accepted, one superseded); eight RuleTwin Phase 1 ADRs pending |
| API | Future RuleTwin OpenAPI and examples in product repo | Not started |
| Data model | Future ERD, migrations, lifecycle/retention doc | Not started |
| CI / clean build | Future workflow runs and clean-clone transcript | Not started |
| Security / isolation | `docs/security/threat-model.md`, future security suite | Threat model initial only; no controls/tests run |
| Supply chain / SBOM | Future pinned dependencies, scans, release SBOM | Not started; no dependencies |
| Observability | Future dashboard, alert/runbook, trace example | Not started |
| Reliability / backup / rollback | Future failure-injection, clean restore and timed drill | Not started |
| Performance / evaluation | Future `evals/reports/` with fixture/hardware/version manifest | Targets defined, no results |
| Accessibility | Future web keyboard/forms/contrast audit | Not started |
| Operations | Future runbooks linked to actionable alerts | Known limitations documented; runbooks not started |
| Economics | Future documented local resource/unit estimate | ₹0 cash target; no measured model |
| Portfolio proof | Root README, demo, case study, defense/evidence | README and plan drafted; no running demo/case study |

Phase 0 documentation was merged through [PR #1](https://github.com/Preethamreddy29/enterprise-rule-intelligence/pull/1) at merge commit `d4c5935`. This closes only the Phase 0 documentation gate; it does not satisfy any runtime or release hard gate below.

## RuleTwin Phase 0 exit audit — 2026-09-27

This is a documentation-gate audit, not product validation or release evidence.

| Runbook exit criterion | Classification | Evidence and limitation |
|---|---|---|
| Problem and user are specific | Satisfied with evidence | `docs/product/charter.md` and `problem-brief.md` define the release manager/configuration workflow and five roles. Role inputs are explicitly simulated hypotheses, not interviews. |
| One measurable critical workflow exists | Satisfied with evidence | `docs/product/prd.md` defines the end-to-end workflow; `metrics.md` defines false-safe, recall, determinism, cycle-time, latency, audit, and isolation measures. No values are reported as measured. |
| Non-goals prevent accidental billing-platform scope | Satisfied with evidence | `docs/product/charter.md` and `prd.md` exclude billing, payments, invoice issuance, arbitrary executable rules, and production changes. |
| Synthetic data can demonstrate tenant differences without employer information | Satisfied with design evidence | `synthetic-data-notice.md` and `synthetic-scenario.md` define three fictional tenants, candidate applicability, affected/no-delta/effective-date expectations, and provenance constraints. Executable fixtures remain Phase 2–3 work. |
| At least three assumptions have falsification tests | Satisfied with evidence | `docs/product/problem-brief.md` records five unverified assumptions, falsification methods, and decisions if falsified. |

No Phase 0 exit criterion is classified as partially satisfied, missing, or requiring a maintainer decision. Repository topology is accepted in ADR-001 and the restored blueprint was reviewed in superseded ADR-002. PR #1 merged the evidence into `main` on 2026-09-27. License, money/date semantics, authentication, retention, risk thresholds, and product-repository creation remain Phase 1 decisions rather than Phase 0 blockers.

## RuleTwin release hard gates

Dangerous false-safe 0; affected-scenario recall >=0.98 target; identical-tuple determinism 100%; protected mutation audit 100%; tenant isolation 100%; self/stale/substituted approval rejection 100%; no lost acknowledged simulation/duplicate under crash; unavailable risk policy fails closed; exact tagged release reproduces signature demo. **All are not started; no evidence links exist yet.**

## Status policy

Use matrix statuses exactly: Not started, In progress, Failed, Passed, Accepted limitation. A row may be marked Passed only from reproducible evidence on the exact release candidate. Security/safety hard gates cannot be accepted as limitations. Update links and commit/tag/hardware/fixture identifiers at every promotion.
