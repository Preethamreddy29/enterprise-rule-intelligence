# RuleTwin Current Journey (Hypothesis)

**Status:** unvalidated workflow hypothesis; no NovaBill process or user was observed.

1. Product owner describes an intended rule/configuration change.
2. Analyst locates current behavior, tenant differences, effective dates, and dependencies across available artifacts.
3. QA selects examples and computes expected outcomes using local knowledge or existing test procedures.
4. Reviewers compare candidate behavior against baseline; coverage and evidence lineage may be difficult to establish.
5. Release manager weighs results, unresolved questions, and operational risk.
6. Decision and rationale are recorded in the tools/process available to the team.
7. Later, an auditor attempts to reconstruct what versions and evidence informed the decision.

### Hypothesized friction to validate

- Unclear tenant/scenario coverage.
- Manual or repeated outcome calculation.
- Rule/version evidence is not bound to a single replay result.
- Effective-date and dependency edge cases are discovered late.
- The same evidence is hard to reproduce later.

These are hypotheses only, not claims about an actual company or existing product.
