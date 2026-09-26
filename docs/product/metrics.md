# RuleTwin Metrics and Evaluation Plan

All values start as definitions/targets. No metric has been measured in this documentation-only phase.

| Metric | Definition | Phase / target | Guardrail and evidence |
|---|---|---|---|
| Dangerous false-safe rate | Dangerous release fixtures producing allow / all dangerous fixtures | Phase 6: 0 | Every dangerous fixture has expected blocked outcome and rationale. Any nonzero blocks release. |
| Affected-scenario recall | Correctly identified expected-affected scenarios / all expected-affected scenarios | Phase 6: >= 0.98 target | Slice by rule family, tenant, date, and consequence; false-safe omissions block regardless of aggregate. |
| Impact precision | Correctly identified affected scenarios / all reported affected scenarios | Report in Phase 6; optimize after recall | A false positive may create review cost; report confusion matrix and reasons. |
| Replay determinism | Identical canonical result checksums / repeated identical tuples | 100% release target | Include engine, rule, dataset, policy versions; repeat across restarts. |
| Decision cycle time | Elapsed time from candidate submission to recorded reviewer outcome | Baseline in scripted usability tasks; compare later | Do not claim time saved without comparable baseline and participant provenance. |
| Reviewer override rate | Policy recommendation changed by authorized reviewer / reviewed simulations | Report, no initial target | Segment by risk class; investigate policy mismatch, never optimize by discouraging safe overrides. |
| Simulation latency | Request acknowledgment and event replay completion P50/P95 | Request ack <750 ms target; 10k completion target set after baseline | Record hardware, concurrency, data size, commit, and resource budget. |
| Audit completeness | Protected mutations with complete required audit evidence / protected mutations | 100% release target | Missing audit event is a release blocker. |
| Tenant isolation | Unauthorized cross-tenant reads/writes returning data or success / tested cases | 0 leakage, full test pass | Exercise paths, filters, exports, artifacts, metrics, and async jobs. |

## Evaluation corpus design (Phase 6)

At least 40 controlled changes: 8 safe/no-effect; 8 tenant-isolated; 6 dependency/cross-rule; 6 date-boundary; 4 rounding/precision; 4 malformed/missing data; 4 dangerous changes that must block. Store fixtures, expected tenant/scenario effects, expected delta class, policy result, rationale, and dataset/evaluator versions. Keep safety slices separately visible.

## Phase evidence

- Phase 0: hypotheses and definitions only.
- Phase 3: golden deterministic rounding cases and property/boundary tests.
- Phase 4: role/tenant and rule-family test matrices.
- Phase 5: adversarial/failure suite.
- Phase 6: reproducible report, confusion matrix, performance/load evidence, hardware and commit metadata.

Do not report a percentage without the fixture set, numerator/denominator, version, and execution evidence.
