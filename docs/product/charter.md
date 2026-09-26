# RuleTwin Charter (Phase 0)

## Problem

NovaBill serves multiple fictional tenants on shared software, but each tenant has distinct rules, effective dates, contracts, and operational data. Reviewing a proposed rule/configuration change from documents or hand-picked examples can miss tenant-specific consequences. A reviewer needs reproducible evidence about what changes before release.

## Users

- **Product owner:** scopes intended behavior and accepts business risk.
- **Configuration analyst:** authors a candidate version and examines tenant/rule dependencies.
- **QA lead:** selects regression scenarios and checks expected behavior.
- **Release manager:** accepts or blocks a release using evidence.
- **Auditor:** reproduces a past decision from exact immutable inputs.

Roles describe product needs, not a claim that interviews have occurred. Discovery hypotheses are separately labeled in the problem brief.

## Value hypothesis

If a reviewer can replay the same versioned event set against the current and candidate rule using a deterministic engine, then the reviewer can identify harmful or tenant-specific impact earlier, reduce manual comparison effort, and support a traceable release decision. This hypothesis must be evaluated; no improvement is yet measured.

## v1 outcome

A reviewer can create a validated immutable candidate rule version, select a reproducible synthetic dataset, compare baseline and candidate outcomes, inspect affected tenants/scenarios and risk reasons, and approve or block based on checksum-bound evidence. Risk evaluation defaults to fail-closed.

## v1 scope

- Five declarative rule families: rounding, tiered rate, late fee, effective-date eligibility, and exception routing.
- Three synthetic tenant configurations with deliberately different behavior.
- Deterministic event generation and replay; baseline/candidate outcome comparison.
- Versioned risk policy and auditable evidence sufficient to reproduce a decision.

Detailed inclusion is in the [PRD](prd.md); implementation is gated by [the phased plan](../implementation-plan.md).

## Non-goals

- Billing, payment collection, invoice issuance, or production financial operations.
- Arbitrary Python/JavaScript evaluation or AI-generated executable rules.
- A general rules authoring/no-code platform, feature-flag system, or production deployment service.
- Direct production-data ingestion or use of non-synthetic employer/client data.
- Automatic approval or release based solely on model output.
- DecisionTrace or BoundaryOps implementation in this milestone.

## Constraints and guardrails

₹0 cash cost; local Docker Compose at implementation; PostgreSQL persistence; strict tenant isolation; immutable rule/evidence versions; deterministic evaluation; API and event contracts versioned; product deployments and databases independent. No paid services or hosted persistent backend.

## Phase 0 success criteria

- One specific user/problem and a measurable critical workflow are documented.
- Non-goals make financial/billing-platform scope explicit.
- A three-tenant synthetic signature scenario and data ownership notice exist.
- At least three assumptions have explicit falsification tests.
- Requirements link to planned code, tests, and evidence in the traceability table.
- No unsupported user-research, performance, security, or readiness claim is made.
