# GitHub Workflow Templates

Copy these into each product repository during Phase 2. Replace product-specific placeholders rather than weakening required sections.

## 1. Pull request template

Place at `.github/pull_request_template.md`.

```markdown
## Outcome

<!-- What user/system outcome does this PR create? -->

Closes: #

## Why

<!-- Problem, evidence, and why now. -->

## Scope

### Included
-

### Excluded
-

## Change summary

- Product behavior:
- API/event contracts:
- Data/migrations:
- UI:
- Worker/infrastructure:

## Acceptance evidence

| Criterion | Evidence |
|---|---|
| | |

## Test evidence

- [ ] Unit/property
- [ ] Integration with PostgreSQL
- [ ] Contract/schema
- [ ] Authorization and tenant isolation
- [ ] End-to-end critical path
- [ ] Product evaluation/regression, if relevant
- [ ] Failure/recovery path

Commands/results:

```text

```

## Security and privacy

- Threat/control changed:
- New data collected/stored/logged:
- Authorization and tenant-scope impact:
- Abuse/failure cases tested:
- Secrets or dependency impact:

## Observability

- Logs:
- Metrics:
- Traces:
- Alert/runbook:

## Deployment and rollback

- Feature flag/default state:
- Migration order:
- Compatibility:
- Smoke test:
- Rollback/forward-fix:
- Data recovery implications:

## Documentation and decisions

- [ ] OpenAPI/schema updated
- [ ] User/operations documentation updated
- [ ] ADR added/updated or not required with reason
- [ ] Risk register/threat model updated or not required with reason

## Reviewer focus

<!-- Name the highest-risk assumption or code path. -->
```

## 2. Feature issue template

Place at `.github/ISSUE_TEMPLATE/feature.yml` or adapt this Markdown into a form.

```markdown
# [Product ID] Feature title

## User and problem

As a [specific user], when [situation], I need [capability], so that [measurable outcome].

## Evidence

Link or summarize problem evidence. Label synthetic assumptions.

## Desired outcome and measure

- Primary metric:
- Guardrail:
- Counter-metric:

## Acceptance criteria

1. Given / When / Then
2. Given / When / Then

## Scope

Included:
-

Excluded:
-

## Roles, tenants, and data

- Allowed roles:
- Denied roles:
- Tenant behavior:
- Data created/read/updated/deleted/retained:

## Failure and abuse cases

- Dependency unavailable:
- Duplicate/retry:
- Stale/concurrent state:
- Unauthorized/cross-tenant request:
- Oversized/malformed/adversarial input:

## Contract and migration impact

- API/event:
- Database:
- Backward compatibility:

## Observability

- Logs:
- Metrics:
- Traces:
- Operator action:

## Test and rollout plan

- Test layers:
- Feature flag:
- Staging scenario:
- Rollback trigger:

## Open questions

- [ ] Question — owner — due date
```

## 3. Bug report template

```markdown
# [Severity] Short defect title

## Observed behavior

## Expected behavior

## Reproduction

1.
2.
3.

## Environment and version

- Commit/tag:
- Compose profile:
- Dataset/corpus/evaluation version:
- Model/config version, if relevant:
- Hardware:

## Impact

- Users/tenants/data/actions affected:
- First known occurrence:
- Frequency:
- Workaround:

## Evidence

- Correlation/trace ID:
- Safe logs/screenshots:
- Relevant metric/evaluation case:

## Initial risk classification

- Severity: S0/S1/S2/S3/S4
- Security/privacy/safety impact:
- Release/rollback recommendation:
```

## 4. Architecture Decision Record template

Place at `docs/decisions/ADR-NNN-short-title.md`.

```markdown
# ADR-NNN: Decision title

- Status: Proposed | Accepted | Superseded | Deprecated
- Date:
- Owners:
- Related issues/PRs:
- Supersedes:

## Context

What problem and constraints force a decision? Include scale, security, cost, team, and portfolio constraints.

## Decision drivers

1.
2.

## Options considered

### Option A

- Benefits:
- Costs/risks:

### Option B

- Benefits:
- Costs/risks:

## Decision

State the chosen option and boundary precisely.

## Consequences

- Positive:
- Negative:
- New risks/controls:
- Operational effect:
- Migration/compatibility effect:

## Evidence and validation

What experiment, benchmark, threat analysis, or constraint supports this decision?

## Revisit triggers

Use measurable triggers, not a vague future date.

## Implementation and rollback

How is the decision introduced, observed, and reversed/superseded?
```

## 5. Release issue template

```markdown
# Release vX.Y.Z

## Scope and compatibility

- Included issues/PRs:
- API/event/schema compatibility:
- Known limitations:

## Required evidence

- [ ] Exact commit required checks passed
- [ ] OpenAPI and contracts validated
- [ ] Migration from previous release passed
- [ ] Product evaluation passed hard gates
- [ ] Tenant/permission suite passed
- [ ] Threat model and dependency/container scans reviewed
- [ ] Load/resource report reviewed
- [ ] Backup restored successfully
- [ ] Rollback rehearsed
- [ ] Dashboards, alerts, and runbooks verified
- [ ] Release notes, SBOM, checksums produced

## Deployment plan

1. Preflight:
2. Backup:
3. Migration:
4. Image promotion:
5. Smoke tests:
6. Observation window:

## Rollback triggers

- S0/S1 defect
- Tenant/permission anomaly
- Safety hard-gate failure
- Migration or audit failure
- Sustained critical SLO breach

## Rollback procedure

1.
2.

## Approval

- Engineering review:
- Product/risk review:
- Release decision and timestamp:
```

## 6. CODEOWNERS starter

For a solo portfolio, this records review responsibility and future ownership; it does not create real separation of duties.

```text
* @your-github-user
/docs/product/ @your-github-user
/docs/security/ @your-github-user
/docs/decisions/ @your-github-user
/db/migrations/ @your-github-user
/.github/workflows/ @your-github-user
/packages/contracts/ @your-github-user
```

## 7. Labels

Create:

- type: `feature`, `bug`, `security`, `documentation`, `evaluation`, `operations`, `architecture`, `debt`;
- severity: `S0` through `S4`;
- phase: `phase-0` through `phase-9`;
- product: `api`, `web`, `worker`, `data`, `policy`, `ai`, `observability`;
- status: `blocked`, `needs-decision`, `needs-evidence`, `ready`, `release-blocker`;
- risk: `tenant-isolation`, `data-loss`, `unsafe-action`, `quality-regression`, `compatibility`.

## 8. Milestones and Project board

Use one milestone per phase, then one release milestone. Board fields:

- Status: Backlog, Ready, In progress, Review, Verify, Done.
- Phase.
- Priority: P0–P3.
- Risk.
- Target release.
- Evidence status.
- Blocked by.

Work-in-progress limits: one major feature in implementation, one in review. This keeps a solo build integrated and reduces abandoned branches.

## 9. Branch and PR lifecycle

1. Create/clarify issue until Definition of Ready passes.
2. Branch from current `main` using issue ID.
3. Add failing test or evaluation fixture where appropriate.
4. Implement smallest vertical change.
5. Run focused checks locally, then full relevant suite.
6. Rebase/update from `main` before opening final review.
7. Open draft PR early for design visibility.
8. Complete evidence, security, migration, observability, and rollback sections.
9. Pass required automated checks.
10. Perform delayed self-review or obtain human review when available.
11. Squash merge with Conventional Commit title.
12. Delete branch, verify `main`, close issue, update roadmap/evidence matrix.

Never combine an unrelated refactor with a feature. If a prerequisite refactor is needed, merge it first as a behavior-preserving PR with tests.

## 10. Suggested GitHub Actions workflow split

- `quality.yml`: formatting, lint, typing, unit tests.
- `integration.yml`: PostgreSQL/pgvector, migration, component/integration tests.
- `contracts.yml`: OpenAPI/JSON Schema and consumer compatibility.
- `security.yml`: secret, dependency, static, container scans.
- `e2e.yml`: Compose critical-path smoke.
- `evaluation.yml`: targeted evaluation on relevant changes; full set on release candidate/manual dispatch.
- `release.yml`: build immutable images, SBOM/checksums, release assets after tag.

Pin third-party GitHub Actions to a full commit SHA for supply-chain safety. Grant each workflow the minimum `permissions` it needs.
