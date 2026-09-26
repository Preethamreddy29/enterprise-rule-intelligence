# Architecture Decision Records

An ADR captures a material choice with context, alternatives, consequences, evidence, revisit triggers, and implementation/rollback notes. Proposed decisions are not treated as accepted policy. Use the template in [the supplied GitHub workflow templates](../05_GITHUB_WORKFLOW_TEMPLATES.md).

- [ADR-001: Repository boundary for this checkout](ADR-001-repository-boundary.md) — accepted; this checkout is the portfolio index/planning repository.
- [ADR-002: Missing lower-precedence blueprint](ADR-002-missing-blueprint.md) — superseded after the blueprint was restored and reviewed on 2026-09-27.

The RuleTwin runbook requires eight additional domain/architecture ADRs during Phase 1. They are deliberately not pre-decided in Phase 0: modular monolith, outbox/broker, tenant schema, relational/graph dependencies, declarative rule representation, result storage/retention, hard-block/warning gate, and local JWT/RBAC/OIDC evolution.
