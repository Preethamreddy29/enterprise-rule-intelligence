# Decision Integrity Portfolio — Release Evidence Matrix

## 1. How to use this file

This is the final audit index. Add a repository-relative link in the Evidence column for every row. A status cannot be marked Passed without reproducible evidence from the exact release candidate.

Statuses: `Not started`, `In progress`, `Failed`, `Passed`, `Accepted limitation`. Security and safety hard gates cannot be accepted as limitations.

## 2. Shared engineering evidence

| Area | Required evidence | Release gate | Status | Evidence |
|---|---|---|---|---|
| Product | Charter, problem evidence, users, measurable outcome, non-goals | Reviewed and current | Not started | |
| Requirements | Critical workflow and acceptance criteria traceability | Every v1 requirement mapped to test/demo | Not started | |
| Architecture | Context/container/sequence diagrams | Match deployed system | Not started | |
| Decisions | Minimum five material ADRs with alternatives and revisit triggers | Accepted | Not started | |
| API | Versioned OpenAPI and examples | Valid and contract-tested | Not started | |
| Data | ERD, lifecycle, retention, deletion, ownership | Constraints/migrations verified | Not started | |
| CI | Exact commit checks | All required checks pass | Not started | |
| Clean build | Clean clone/start/test transcript | Reproducible | Not started | |
| Security | Threat model and test mapping | No unmitigated high risk | Not started | |
| Isolation | Role/tenant matrix | 100% pass | Not started | |
| Supply chain | Dependency/container scan and SBOM | No unresolved critical finding | Not started | |
| Observability | Dashboard, alerts, trace example | Critical flow diagnosable | Not started | |
| Reliability | Failure-injection report | No false success/data loss | Not started | |
| Backup | Backup and clean restore transcript | Successful | Not started | |
| Rollback | Timed deployment rollback drill | Successful | Not started | |
| Performance | Versioned load report with hardware | Within documented budget | Not started | |
| Accessibility | Keyboard/forms/contrast/basic screen-reader audit | No critical failure | Not started | |
| Operations | Incident runbooks | Every actionable alert mapped | Not started | |
| Economics | Resource/unit-cost model | Assumptions labeled | Not started | |
| Portfolio | README, demo, case study, limitations, defense | Complete | Not started | |

## 3. RuleTwin hard gates

| Evidence | Threshold | Status | Link |
|---|---:|---|---|
| Dangerous-change false-safe rate | 0 | Not started | |
| Affected-scenario recall | >= 0.98 target | Not started | |
| Same-version replay determinism | 100% | Not started | |
| Protected mutation audit completeness | 100% | Not started | |
| Cross-tenant isolation | 100% | Not started | |
| Self/stale/substituted approval rejection | 100% | Not started | |
| Worker crash/idempotency suite | No duplicate/lost acknowledged simulation | Not started | |
| Risk policy unavailable | Fails closed | Not started | |
| Signature demo reproduction | Exact released version | Not started | |

## 4. DecisionTrace hard gates

| Evidence | Threshold | Status | Link |
|---|---:|---|---|
| Permission-denial accuracy | 100% | Not started | |
| Citation ID validity and authorization | 100% | Not started | |
| Prompt-injection policy bypass | 0 | Not started | |
| Deleted/revoked evidence retrievability | 0 | Not started | |
| Supported-claim rate | >= 0.95 target | Not started | |
| Temporal answer accuracy | >= 0.90 target, sliced | Not started | |
| Abstention accuracy | >= 0.90 target | Not started | |
| Correction/supersession distinction | Full fixture pass | Not started | |
| Source restore and index rebuild | Successful | Not started | |
| Signature demo reproduction | Exact released versions | Not started | |

## 5. BoundaryOps hard gates

| Evidence | Threshold | Status | Link |
|---|---:|---|---|
| Unsafe/prohibited action prevention | 100% | Not started | |
| Cross-tenant leakage | 0 | Not started | |
| Approval replay acceptance | 0 | Not started | |
| Preview/action mismatch | 0 | Not started | |
| Duplicate side effect under crash/retry | 0 | Not started | |
| Executed actions with verification | 100% | Not started | |
| Claimed-reversible action rollback | 100% release suite | Not started | |
| Required-escalation recall | >= 0.98 target | Not started | |
| Write kill switch | Full drill pass | Not started | |
| Signature demo reproduction | Exact released versions | Not started | |

## 6. Cross-project integration gates

| Check | Expected result | Status | Evidence |
|---|---|---|---|
| BoundaryOps ↔ RuleTwin contract | Consumer/provider tests pass | Not started | |
| BoundaryOps ↔ DecisionTrace contract | Consumer/provider tests pass | Not started | |
| Tenant propagation | Same authenticated tenant enforced end-to-end | Not started | |
| Correlation propagation | One trace links case, query, simulation, and action | Not started | |
| Upstream timeout | BoundaryOps escalates; no action | Not started | |
| Stale RuleTwin result | Preview/approval invalidated | Not started | |
| Conflicting DecisionTrace evidence | Escalation; no action | Not started | |
| Upstream major-version incompatibility | Readiness fails closed | Not started | |
| Integrated backup/restore | Recovered state remains consistent | Not started | |
| Integrated signature demonstration | Full proof-before-action flow succeeds | Not started | |

## 7. Final product-management evidence

For each product, link:

- the user/problem decision and what was deliberately excluded;
- three alternatives rejected and why;
- success metric, guardrail, and counter-metric;
- observed evaluation results and one decision changed by evidence;
- reliability/security trade-off;
- unit economics and scale-evolution trigger;
- current limitation and next experiment;
- 60-second, five-minute, and 30-minute narratives.

The portfolio is complete only when the evidence demonstrates **BUILD → DECIDE → MEASURE → DEFEND**, not merely when the applications run.
