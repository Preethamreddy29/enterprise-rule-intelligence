# Known Limitations and Open Questions

## Current limitations (2026-10-26)

- This repository is a portfolio index and contains no product runtime. RuleTwin and DecisionTrace code, product contracts, tests and exact validation records live in separate repositories.
- No real users or customers were interviewed. All five role inputs are synthetic hypotheses, not empirical discovery evidence.
- RuleTwin is a validated local synthetic-data demonstration, not an externally hosted pilot or production-ready service. Its first three phases and bounded Phase 4A increment are complete, but the original full Phase 4–8 gates remain open.
- RuleTwin currently supports one deterministic rounding family and two fictional tenants. Four planned rule families, a third tenant, dependency analysis, richer impact dimensions, webhook delivery, evidence reproduction and pagination are incomplete.
- RuleTwin's provider-neutral OIDC verification foundation is awaiting merge in PR #22. Provider-specific browser login/logout, pilot-user provisioning and real-provider evidence are incomplete.
- Full exposed-surface isolation, resource/rate controls, centralized alerts, hosted deployment, external secret storage, backup/restore/rollback, SBOM/release artifacts, accessibility, the 40+ case evaluation corpus and reference-profile performance remain open.
- No RuleTwin release candidate, immutable product release, tagged evidence contract or `v1.0.0` exists. Slice-level evidence must not be presented as passing a full release hard gate.
- DecisionTrace is being developed independently under a maintainer-approved parallel exception. RuleTwin/DecisionTrace integration remains prohibited until stable versioned contracts and consumer tests exist.
- BoundaryOps runtime remains prohibited until both upstream products have stable tagged contracts, examples and passing mock consumer tests.
- The ₹0 target excludes unplanned paid dependencies/cloud services, but local hardware/electricity and any future hosting/domain/identity-provider costs must be disclosed.

## Mitigation and decision gates

- Keep slice, pilot, phase and production claims distinct and linked to exact evidence.
- Keep runtime and product-owned contracts in the separate product repositories; this repository records governance and milestone summaries.
- Update portfolio status after every product milestone so the index does not lag implementation.
- Resolve hosting, domain/TLS, invited identities/roles, backup retention, RPO/RTO, availability and visibility before closing the RuleTwin pilot deployment gate.
- Require clean-runner CI, tenant-isolation, recovery, security, performance, accessibility and immutable release evidence before promotion.
- Never relax hard tenant-isolation, unsafe execution, dangerous false-safe, audit, or approval gates to satisfy a demo.

## Change log

Update on each milestone; move resolved items to progress/ADR history rather than erasing the decision trail.
