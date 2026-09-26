# Testing Strategy and Verification Commands

## Current Phase 0

There is no application/tooling or test suite yet. No test command is claimed to have passed. Documentation checks in this milestone are link/file inventory and Git diff/status review; they do not validate runtime behavior.

## Planned test layers

| Layer | Purpose | Planned location / gate |
|---|---|---|
| Unit/property | Rule canonicalization, arithmetic/date boundaries, pure comparison and policy invariants | `tests/unit/`, Phase 3 onward |
| Component | API/application behavior with controlled adapters | `tests/component/`, Phase 2–4 |
| PostgreSQL integration | migrations, transactions, tenant scoping, outbox leasing/idempotency | `tests/integration/`, real ephemeral PostgreSQL in CI |
| Contract | OpenAPI validity and provider/consumer compatibility; JSON Schema event validation | `tests/contract/`, each public contract change |
| Security | role-action matrix, tenant isolation, hostile rule/resource limits, audit controls | `tests/security/`, every critical change/release |
| Performance | 1k/10k/100k event profiles and noisy-tenant tests with named hardware | `tests/performance/`, Phase 6 |
| End-to-end | propose → replay → impact → review/approve-or-block and reproduction | `tests/e2e/`, Phase 3 onward |
| Recovery | API/worker/database crash points, backup restore, rollback | Phase 5–8 |
| Evaluation | at least 40 versioned safe, boundary, malformed, dependency, dangerous changes | `evals/fixtures/`, `evals/expected/`, Phase 6 |

## Required proof discipline

Record exact command, commit/tag, test set, exit status, and relevant output. Do not label a test passed before it has run. Never aggregate away dangerous false-safe or tenant-isolation failures. Reproducibility reports identify engine, rule, dataset/generator, risk-policy versions, hardware, and fixture manifest.

## Future clean-checkout gate

During Phase 2, add one command sequence for formatting/lint, static types, unit, integration, contract/schema, security, build, and clean Compose smoke checks. Add real PostgreSQL migration tests and container checks. This file will be updated only after actual commands exist and run.
