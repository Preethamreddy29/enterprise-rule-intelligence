# ADR-002: Missing Lower-Precedence Blueprint

- Status: Superseded on 2026-09-27 (blueprint restored and reviewed)
- Date: 2026-09-26; superseded 2026-09-27
- Owners: Repository maintainer
- Related: user-requested authoritative document list; docs/README.md

## Context

The required file `docs/Technical_Product_Portfolio_Project_Blueprint.md` is not present in the complete checkout inventory. The available `docs/README.md`, handbook, all three product runbooks, release evidence matrix, and workflow templates were read. The handbook explicitly establishes precedence over the blueprint; the RuleTwin runbook is authoritative for the active product sequence and Phase 0 work.

On 2026-09-27 the blueprint became available at the required path. It was reviewed under the established precedence order. Its portfolio thesis, separate-repository model, RuleTwin-first sequence, synthetic-data constraint, five RuleTwin rule families, three-tenant scope, and ₹0 stack are consistent with the higher-precedence handbook and RuleTwin runbook. No material conflict requiring an ADR was found.

## Decision drivers

1. Do not fabricate or infer text from an absent document.
2. Honor document precedence and continue only where available higher-precedence documents provide sufficient direction.
3. Keep ambiguity visible and avoid irreversible runtime/repository decisions.

## Options considered

### Block all work until the blueprint is supplied

- Benefits: all requested sources could be reviewed first.
- Costs/risks: prevents safe charter, traceability, and risk documentation already defined by higher-precedence sources.

### Proceed with available higher-precedence sources and disclose the omission

- Benefits: enables reversible Phase 0 planning while preserving precedence.
- Costs/risks: there may be lower-precedence project context not yet visible.

## Decision

The original decision—to proceed reversibly with higher-precedence sources while disclosing the missing blueprint—was valid for the 2026-09-26 Phase 0 draft. It is now superseded. Retain this ADR as decision history, remove the blueprint absence as an active blocker, and use the restored blueprint as lower-precedence context.

## Consequences

- Phase 0 artifacts have now been checked against all named sources.
- Repository topology is resolved separately in ADR-001.
- No product code or release claim is authorized by this decision.

## Evidence and validation

The 2026-09-26 inventory established the original absence. The 2026-09-27 inventory found the blueprint at the requested path; comparison against the handbook and RuleTwin runbook found no material conflict.

## Revisit triggers

A material conflict with a higher-priority document is discovered, or the blueprint changes. Precedence remains handbook → relevant runbook → evidence matrix → blueprint → repository README.

## Implementation and rollback

No code changes are required. This documentation update closes the missing-source limitation; later blueprint changes must be reviewed through normal traceability and ADR maintenance.
