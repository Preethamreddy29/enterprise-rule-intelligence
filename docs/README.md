# Decision Integrity Portfolio — Execution Documents

Use the documents in this order:

1. [`00_PORTFOLIO_ENGINEERING_HANDBOOK.md`](00_PORTFOLIO_ENGINEERING_HANDBOOK.md) — rules shared by every repository.
2. [`01_RULETWIN_IMPLEMENTATION_RUNBOOK.md`](01_RULETWIN_IMPLEMENTATION_RUNBOOK.md) — build and release first.
3. [`02_DECISIONTRACE_IMPLEMENTATION_RUNBOOK.md`](02_DECISIONTRACE_IMPLEMENTATION_RUNBOOK.md) — build after RuleTwin v1.
4. [`03_BOUNDARYOPS_IMPLEMENTATION_RUNBOOK.md`](03_BOUNDARYOPS_IMPLEMENTATION_RUNBOOK.md) — build after both upstream APIs stabilize.
5. [`04_RELEASE_EVIDENCE_MATRIX.md`](04_RELEASE_EVIDENCE_MATRIX.md) — final audit and evidence index.
6. [`Technical_Product_Portfolio_Project_Blueprint.md`](Technical_Product_Portfolio_Project_Blueprint.md) — lower-precedence portfolio rationale, scope, and sequencing context.

The runbooks define phase order, deliverables, implementation work, tests, security controls, deployment promotion, and exit gates. The handbook owns Git, PR, architecture, security, reliability, and documentation standards. The blueprint supplies lower-precedence portfolio context. If sources conflict, use the higher-precedence source or the stricter safety or quality requirement and record the decision in an ADR.

This plan targets a credible local production release at zero cash cost. It does not promise zero defects; it makes defects harder to introduce, easier to detect, and safer to recover from.
