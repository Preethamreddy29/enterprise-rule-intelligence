# RuleTwin Problem Brief

## Problem statement

A product/configuration team changing a shared billing rule must reason about tenant-specific contracts, effective dates, dependencies, and historical events. Existing review evidence may be incomplete or non-repeatable. A change that seems correct for one tenant may produce a different financial amount, workflow state, error, event, or timing for another. RuleTwin will make those differences visible before release; it will not change production rules.

## Consequence

A missed regression can cause incorrect billing behavior, operational exceptions, delayed releases, customer-impacting corrections, or loss of confidence in review evidence. These are plausible risks to validate, not observed NovaBill incidents.

## Job to be done

When I propose a business-rule/configuration change, I need to replay representative, versioned events under current and candidate behavior and see reproducible tenant-level deltas, so that I can decide whether to approve, revise, or block the change with evidence.

## Current-state hypothesis (not observed research)

Review may rely on manual document comparison, targeted examples, and reviewer knowledge distributed across roles. The actual current process is unknown. Phase 0 simulated role prompts in this document are not interviews or customer evidence.

## Desired state

1. Analyst records a candidate as validated declarative data.
2. Reviewer selects a known, checksummed dataset and policy version.
3. Current and candidate rules run in isolated deterministic contexts.
4. Reviewer sees tenant/scenario deltas, uncertainty/coverage, and a fail-closed risk outcome.
5. An authorized human decision is bound to immutable result evidence.
6. Auditor can reproduce the exact result tuple later.

## Discovery prompts and simulated role hypotheses

**Evidence label: synthetic discovery exercise.** No people were interviewed. These are role-based hypotheses generated to guide later real or simulated validation; they must not be presented as findings from users.

| Role | Structured prompts | Simulated hypothesis to test |
|---|---|---|
| Product owner | How is intended behavior stated? What evidence changes your decision? Which unintended impact is most costly? | Wants a concise explanation by tenant and consequence, not raw event dumps. |
| Configuration analyst | How are rule versions and dependencies found? What inputs are often missing? | Wants validation errors and a diff before spending time on a large replay. |
| QA lead | How are regression cases selected and expected results maintained? How are boundaries covered? | Wants stable fixtures, boundary cases, and a reproducible run identifier. |
| Release manager | What blocks/permits a release? How do you handle incomplete evidence? | Wants explicit policy reasons, fail-closed behavior, and a human override trail rather than an opaque score. |
| Auditor | What must be retained to reproduce a decision? How do you know evidence was not substituted? | Wants immutable rule/data/policy/engine versions and checksums tied to the approval. |

## Falsifiable assumptions

| ID | Assumption (unverified) | Falsification method | Decision if falsified |
|---|---|---|---|
| A1 | Reviewers need tenant-level outcome deltas to identify risk more effectively than a single aggregate. | Scripted three-tenant task; compare error detection and explanation quality with aggregate-only versus tenant-level views. Label pilot results synthetic unless real participants consent. | Simplify presentation if detail does not improve decisions; retain tenant scope as a security boundary regardless. |
| A2 | Deterministic replay inputs can be captured as a bounded, versioned synthetic dataset representative enough for a portfolio demonstration. | Build boundary and malformed fixtures; ask reviewers to identify missing categories; compare expected and computed outputs. | Narrow supported rule/event model and state coverage limitations. |
| A3 | A versioned deterministic policy can express a useful allow/block decision without an AI decision-maker. | Define dangerous/safe fixture set and test whether policy reasons are understandable and dangerous cases never pass. | Keep recommendation-only mode or refine policy; never relax a safety gate to improve demo success. |
| A4 | Review evidence can be reproduced from exact engine, rule, dataset, and policy versions. | Repeat identical tuples across clean database/process restarts and compare canonical checksums. | Block reproducibility claims and release until source of nondeterminism is resolved. |
| A5 | A focused MVP needs the five specified declarative rule families. | Map each scripted workflow to rule family and collect reviewer feedback; remove unsupported types before implementation. | Narrow v1 scope; do not claim unsupported semantics. |

## Evidence plan

Phase 0 evidence is limited to documented scenario design and simulated hypotheses. Phase 3 adds executable unit/property tests and one-tenant golden replay. Phase 4 adds cross-tenant, role, failure, and UI workflow tests. Phase 6 publishes fixture-level accuracy/determinism reports. Nothing is measured until those tests are implemented and run.
