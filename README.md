# Decision Integrity Infrastructure for Configurable B2B SaaS

A zero-cash-cost portfolio project for safer, explainable changes in NovaBill, a fictional multi-tenant contract-to-cash and utility-billing SaaS.

> **Current state:** RuleTwin Phase 0 is closed as a documentation gate, and Phase 1 design is next. No API, UI, worker, database, or deployable product exists yet. Nothing here should be represented as production-ready.

## Product sequence

1. **RuleTwin** — replay historical or deterministic synthetic events against current and proposed tenant-specific rules; compare outcomes and produce review evidence.
2. **DecisionTrace** — later, reconstruct time-aware decisions from versioned evidence and detect contradictions, supersession, correction, and drift. Not started.
3. **BoundaryOps** — later, investigate exceptions using only versioned RuleTwin/DecisionTrace contracts; deterministic code controls authorization, approvals, actions, verification, rollback, budgets, and termination. Not started. Runtime work is blocked until both upstream v1 contracts and mock consumer tests exist.

The portfolio is fictional, synthetic-data-only, and unaffiliated with any employer or customer. See [the synthetic-data notice](docs/product/synthetic-data-notice.md).

## Current milestone

Establish the separate RuleTwin repository and complete Phase 1 domain, data, API, architecture, threat, policy, and tenant/RBAC design there. This repository remains the portfolio index and milestone record. Start with the [progress log](docs/progress.md), [implementation plan](docs/implementation-plan.md), and [requirements traceability](docs/requirements-traceability.md).

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

This milestone is documentation-only. No environment variables, runtime services, or Python/Node dependencies are required. The `.env.example` intentionally contains no credentials or invented runtime configuration. See [local setup](docs/architecture/local-setup.md) for the planned development environment and future clean-clone gate.

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
