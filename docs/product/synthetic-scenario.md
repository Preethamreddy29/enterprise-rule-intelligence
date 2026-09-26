# NovaBill Synthetic Signature Scenario (Design)

**Status:** scenario specification only. No fixtures or outcomes have been generated or executed.

## Purpose

Show how one proposed rule change on shared software can have distinct effects across tenant-specific settings, and show both impact and a no-change control using reproducible synthetic events.

## Synthetic entities

- Tenant identifiers: `tenant-amber`, `tenant-cobalt`, `tenant-jade` (fictional opaque IDs).
- Each has a separately versioned configuration and effective-date schedule; they share the same application and event schema.
- Event cohort contains generated contract/account events with exact fixed-seed values and timestamps; no external extracts.

The following configurations are Phase 0 scenario inputs, not implemented or measured behavior. Exact money, date, and rule-schema semantics remain Phase 1 decisions.

| Tenant | Current configuration | Candidate applicability | Expected qualitative result |
|---|---|---|---|
| `tenant-amber` | Line-level half-up rounding; late fee depends on the rounded subtotal; standard eligibility and exception routing. | Candidate half-even rounding applies on the scenario effective date. | Boundary events may change rounded amount, late-fee input, and downstream exception route; risk policy must review the linked deltas. |
| `tenant-cobalt` | Tenant override retains half-up rounding; a distinct tier schedule and late-fee threshold remain otherwise unchanged. | Candidate is not enabled for this tenant. | No delta control: identical baseline and candidate outcomes are expected for valid events. |
| `tenant-jade` | Half-up rounding with a separately versioned eligibility window and exception threshold. | Candidate half-even rounding is scheduled for a later effective date. | Pre-effective events remain unchanged; events at/after the candidate date may change, proving effective-time selection. |

Across the portfolio fixture design, the five rule families are rounding, tiered rate, late fee, effective-date eligibility, and exception routing. This signature scenario emphasizes rounding, its late-fee dependency, effective dates, and exception routing; separate later fixtures cover tiered-rate behavior directly.

## Proposed scenario

Candidate revision changes a supported rounding policy in a controlled way. Replay the exact same event cohort through the current and candidate rule versions for each tenant. Fixtures must include amounts near rounding boundaries, multiple line items, exact-cent controls, missing/malformed inputs, and effective-time boundaries. Expected behavior is to identify affected `tenant-amber` boundary cases, preserve `tenant-cobalt` as a no-delta control, distinguish `tenant-jade` pre-effective and post-effective cohorts, and ensure malformed/budget-exceeding inputs do not silently pass.

## Evidence produced by future evaluator

Manifest with generator version/seed, tenant/rule versions, engine and risk-policy version, input/output checksums, expected and observed deltas, coverage, and policy reasons. Reviewer can reproduce all outcomes from the manifest. The risk policy blocks any dangerous outcome in the release fixture set.

## Acceptance of fixture before implementation completion

- All values and identities are obviously synthetic.
- Three tenants differ only through documented fictional config, not hidden evaluator branches.
- Golden expected outcomes are independently reviewed and tests exercise both change and control tenants.
- Dates, currency minor units/decimal semantics, tie-breaking and rounding mode are explicit and agreed in Phase 1.
- No scenario result is described as a real customer impact or measured value.
