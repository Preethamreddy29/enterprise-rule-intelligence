# Decision Integrity Infrastructure for Configurable B2B SaaS

A zero-cash-cost portfolio project for safer, explainable changes in NovaBill, a fictional multi-tenant contract-to-cash and utility-billing SaaS.

> **Current state:** RuleTwin Phases 0–3 and the bounded Phase 4A tenant-authorization increment are complete in its [separate repository](https://github.com/Preethamreddy29/ruletwin). Tenant-authorized evidence export is merged, and a provider-neutral OIDC verification foundation is awaiting merge in [PR #22](https://github.com/Preethamreddy29/ruletwin/pull/22) with all five CI checks passing. RuleTwin is a validated synthetic-data local demonstration, not an externally hosted pilot or production-ready service. DecisionTrace also continues independently; the products are not integrated.

## Product sequence

1. **RuleTwin** — replay historical or deterministic synthetic events against current and proposed tenant-specific rules; compare outcomes and produce review evidence.
2. **DecisionTrace** — standalone work began in its [separate repository](https://github.com/Preethamreddy29/decisiontrace) on 2026-10-23. Its Phase 0 corpus, Phase 1 design, and narrowed Phase 2 local foundation gates are complete. Its current synthetic preview and remaining completion gates are summarized in the [DecisionTrace completion plan](docs/05_DECISIONTRACE_COMPLETION_PLAN.md). The full Phase 3 and Phase 4 gates and RuleTwin integration remain open.
3. **BoundaryOps** — later, investigate exceptions using only versioned RuleTwin/DecisionTrace contracts; deterministic code controls authorization, approvals, actions, verification, rollback, budgets, and termination. Not started. Runtime work is blocked until both upstream v1 contracts and mock consumer tests exist.

The portfolio is fictional, synthetic-data-only, and unaffiliated with any employer or customer. See [the synthetic-data notice](docs/product/synthetic-data-notice.md).

## Current milestone

Finish RuleTwin's controlled synthetic-data pilot without claiming that the original full Phase 4–8 gates are closed. The immediate sequence is: merge the validated OIDC foundation, complete provider login/logout, prove full exposed-surface isolation and resource controls, add operations/deployment/recovery evidence, and publish a pilot release only after its gate passes. The remaining four rule families and full-v1 breadth follow as separate Phase 4 work. This repository remains the portfolio index and milestone record. Start with the [progress log](docs/progress.md), [implementation plan](docs/implementation-plan.md), and [requirements traceability](docs/requirements-traceability.md).

## Documentation

- [Architecture and product boundaries](docs/architecture/portfolio-boundaries.md)
- [Proposed repository layout](docs/architecture/repository-layout.md)
- [Local setup](docs/architecture/local-setup.md)
- [Testing strategy](docs/architecture/testing.md)
- [Threat model](docs/security/threat-model.md)
- [ADRs](docs/decisions/)
- [Known limitations](docs/operations/known-limitations.md)
- [Release evidence index](docs/release/evidence-index.md)
- [Execution documents](docs/README.md)

## Local use today

This portfolio repository remains documentation-only. The runnable products live in their own repositories. RuleTwin currently provides a Docker Compose local demonstration of its deterministic rounding workflow, authorization boundary, audit trail, and evidence export; its exact setup and validation instructions are owned by the RuleTwin repository. The portfolio `.env.example` intentionally contains no product credentials.

## Engineering constraints

- ₹0 cash-cost target; no paid APIs or hosted backends.
- React + TypeScript + Vite, Python + FastAPI, PostgreSQL, and Docker Compose at the implementation phase.
- Separate independently testable/deployable products and databases; no direct cross-product database access.
- OpenAPI for synchronous APIs; JSON Schema for events; outbox and worker where asynchronous processing is required.
- Tenant identity is server-derived and tenant-owned data is isolated.
- Rule input is declarative and interpreted deterministically; never execute user-supplied code.
- BoundaryOps remains bounded and policy-governed; an LLM cannot authorize or perform consequential actions.
- No secrets, real customer information, or employer/client materials in source.

## Status and claims

The release evidence matrix is a checklist, not proof of completion. Every test, performance result, interview, release, and production claim must be backed by reproducible evidence. Simulated discovery notes are hypotheses—not real-user research. See [known limitations](docs/operations/known-limitations.md).
