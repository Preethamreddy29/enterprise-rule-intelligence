# ADR-001: Repository Boundary for This Checkout

- Status: Accepted
- Date: 2026-09-26; accepted 2026-09-27
- Owners: Repository maintainer
- Related: RuleTwin runbook Phase 2; engineering handbook §2, §18

## Context

The handbook specifies four separate repositories (portfolio index, RuleTwin, DecisionTrace, BoundaryOps) and forbids a monorepo. This checkout is named `enterprise-rule-intelligence`, has no commit baseline, and contains the execution sources plus portfolio/RuleTwin Phase 0 planning documents. On 2026-09-27 the maintainer explicitly directed that this repository be treated as the portfolio index and planning repository, with RuleTwin, DecisionTrace, and BoundaryOps kept in separate independently deployable repositories. The lower-precedence blueprint is now present and agrees with that boundary.

## Decision drivers

1. Respect independent deployability, database ownership, and no-monorepo rule.
2. Preserve untracked user-provided documents and avoid building the wrong product in the wrong repository.
3. Make useful, reversible Phase 0 progress without adding runtime coupling or code prematurely.

## Options considered

### A. Implement all products beneath this root

- Benefits: single checkout and apparent completeness.
- Costs/risks: directly violates separate repositories and sequence; creates cross-product coupling; rejected.

### B. Treat root immediately as the RuleTwin product repository

- Benefits: allows standard RuleTwin app layout in this checkout.
- Costs/risks: repository role is unconfirmed; could turn a portfolio repository into a product repo and misplace supplied shared docs.

### C. Keep this checkout as the portfolio index and planning repository

- Benefits: preserves existing work and boundaries; enables charter, traceability, risk, and plan deliverables now.
- Costs/risks: product-specific documents must be intentionally transferred or adapted into the owning product repository without creating runtime coupling.

## Decision

Accept option C. This checkout is the portfolio index and planning repository. Do not scaffold RuleTwin, DecisionTrace, or BoundaryOps runtime here. Establish a separate RuleTwin repository before RuleTwin Phase 2; later products also receive separate repositories. No direct database or internal-package integration will be introduced.

## Consequences

- Positive: no premature monorepo; Phase 0 remains actionable; no existing untracked docs are overwritten.
- Negative: the current checkout will not run an application.
- Risks/controls: accidental runtime work in the portfolio index remains possible; repository layout, progress, and review gates identify it as prohibited.
- Migration: copy or adapt only reviewed RuleTwin-owned planning artifacts into the separate RuleTwin repository with provenance preserved; do not delete portfolio source documents.

## Evidence and validation

Repository inventory and Git status show an unborn branch with all content untracked. The handbook and restored blueprint both require a portfolio index plus separate product repositories. The maintainer's 2026-09-27 instruction resolves this checkout's role as the portfolio index.

## Revisit triggers

- The maintainer intentionally changes the portfolio repository model.
- A higher-precedence source requires a different compatible boundary.
- Measured cross-repository maintenance cost justifies revisiting neutral duplicated templates; product runtime and databases still remain independent.

## Implementation and rollback

Portfolio and Phase 0 planning documents stay in this workspace. The separate RuleTwin repository will own RuleTwin runtime, product contracts, tests, and deployment evidence. Any reversal requires a new ADR; do not copy application code between products or share databases.

Implementation status on 2026-09-27: the supplied portfolio sources were committed as the `main` baseline and pushed to the configured remote. Phase 0 planning remains on `docs/portfolio-foundation-ruletwin-phase0`; no product runtime was added.
