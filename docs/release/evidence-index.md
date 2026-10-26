# Release Evidence Index

The authoritative thresholds and rows are in [the release evidence matrix](../04_RELEASE_EVIDENCE_MATRIX.md). This portfolio repository has no runtime or test suite; exact product evidence lives in the separate product repositories. Phase and slice evidence below must not be interpreted as an exact-release-candidate pass.

| Matrix area | Planned evidence location | Current state |
|---|---|---|
| Product / problem | `docs/product/charter.md`, `problem-brief.md`, journeys, PRD | Phase 0 documentation gate satisfied; role research is simulated only |
| Requirements traceability | `docs/requirements-traceability.md` plus product traceability | Portfolio summary updated; exact RuleTwin code/test mappings live in the product repository |
| Architecture | `docs/architecture/portfolio-boundaries.md`, repository layout; RuleTwin architecture docs | Portfolio boundary and RuleTwin modular-monolith design implemented for the current slice |
| Decisions (minimum five material ADRs) | Portfolio `docs/decisions/`; RuleTwin `docs/decisions/` | Portfolio boundary ADRs plus ten RuleTwin product ADRs exist |
| API | RuleTwin `packages/contracts/openapi.json` and `docs/api/` | Twelve operations validate on PR #22; contract is not yet frozen or tagged |
| Data model | RuleTwin data-model docs and three reversible migrations on PR #22 | Current slice schema implemented; retention and release-candidate upgrade evidence pending |
| CI / clean build | RuleTwin GitHub Actions and validation records | Five clean-runner jobs pass on PR #22 at `1a4c240`; no release candidate exists |
| Security / isolation | Portfolio threat model; RuleTwin threat-to-test and authorization evidence | Phase 4A implemented surfaces and OIDC invalid-token matrix pass; full exposed-surface gate pending |
| Supply chain / SBOM | RuleTwin pinned dependencies, scans and future release SBOM | Dependency/static/secret/container checks exist; release SBOM and immutable artifacts pending |
| Observability | RuleTwin structured logs, health and Prometheus baseline; future alerts/runbooks | Foundation implemented; centralized telemetry and actionable alert evidence pending |
| Reliability / backup / rollback | Future failure-injection, clean restore and timed drill | Not started |
| Performance / evaluation | Future `evals/reports/` with fixture/hardware/version manifest | Targets defined, no results |
| Accessibility | Future web keyboard/forms/contrast audit | Not started |
| Operations | Future runbooks linked to actionable alerts | Known limitations documented; runbooks not started |
| Economics | Future documented local resource/unit estimate | ₹0 cash target; no measured model |
| Portfolio proof | Root README; RuleTwin demo guides; future case study, economics and defense/evidence | Running local RuleTwin demonstration exists; final case study and release defense pending |

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

## RuleTwin current product evidence — 2026-10-26

- Phases 1–3 and bounded Phase 4A are complete in the separate RuleTwin repository.
- Tenant-authorized evidence export is merged through PR #21 at `257e604`.
- [PR #22](https://github.com/Preethamreddy29/ruletwin/pull/22) at `1a4c240` adds the provider-neutral OIDC verification foundation; all five CI checks pass, but the PR remains unmerged.
- Current branch evidence records 58 backend tests, 90.46% backend coverage, three web component tests, 88.31% web statement coverage, two Chromium workflows, valid 12-operation OpenAPI, reversible migrations and zero schema drift.
- Only the deterministic rounding family and two fictional tenants are implemented. Provider login/logout, full-surface isolation, limits, hosted deployment, secrets, backup/restore/rollback, alerts, SBOM, accessibility and reference-profile performance remain open.

## RuleTwin release hard gates

Dangerous false-safe 0; affected-scenario recall >=0.98 target; identical-tuple determinism 100%; protected mutation audit 100%; tenant isolation 100%; self/stale/substituted approval rejection 100%; no lost acknowledged simulation/duplicate under crash; unavailable risk policy fails closed; exact tagged release reproduces signature demo. Slice tests provide partial evidence for determinism, audit, authorization, approvals, worker recovery and fail-closed behavior, but **none of these full release-candidate hard gates is marked Passed because no exact release candidate exists.**

## Status policy

Use matrix statuses exactly: Not started, In progress, Failed, Passed, Accepted limitation. A row may be marked Passed only from reproducible evidence on the exact release candidate. Security/safety hard gates cannot be accepted as limitations. Update links and commit/tag/hardware/fixture identifiers at every promotion.
