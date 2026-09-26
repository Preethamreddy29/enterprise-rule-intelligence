# Known Limitations and Open Questions

## Current limitations (2026-09-27)

- Phase 0 is closed only as a documentation gate. No application code, API, UI, worker, PostgreSQL schema, migrations, seed generator, tests, Compose stack, CI, telemetry, or release exists.
- The portfolio source baseline and Phase 0 documentation are merged into the default `main` branch through PR #1. The PR used a merge commit rather than the planned squash; history is retained and future merge policy must prevent recurrence.
- The blueprint is present and reviewed; ADR-002 retains the earlier missing-source decision as superseded history.
- No real users or customers were interviewed. All five role inputs are synthetic hypotheses, not evidence.
- No performance, accuracy, cost, security, isolation, reliability, restore, or release gate has been measured or passed.
- License, maintainer ownership/review, local authentication/session design, money representation, date/timezone and effective-date semantics, retention, large-result artifact storage, exact REST schemas, risk thresholds, and dataset realism remain design decisions.
- ₹0 target excludes unplanned paid dependencies/cloud services but real local hardware/electricity has an opportunity cost; later cost model should disclose assumptions.
- No RuleTwin contract is published; BoundaryOps integration is prohibited until RuleTwin and DecisionTrace tagged v1 contracts/examples and mock consumer contract tests exist.

## Mitigation and decision gates

- Keep all runtime behavior and completion claims explicitly marked planned.
- Keep runtime and product-owned contracts out of this portfolio index; establish the separate RuleTwin repository before authoritative Phase 1 artifacts are created.
- Obtain explicit approval before any commit, push, repository creation, pull request, or GitHub setting change.
- Resolve Phase 1 design questions with ADRs, threat-to-test mapping, OpenAPI, data model, and evidence.
- Never relax hard tenant-isolation, unsafe execution, dangerous false-safe, audit, or approval gates to satisfy a demo.

## Change log

Update on each milestone; move resolved items to progress/ADR history rather than erasing the decision trail.
