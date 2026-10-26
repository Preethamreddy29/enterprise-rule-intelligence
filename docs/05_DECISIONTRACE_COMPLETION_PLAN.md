# DecisionTrace completion plan and runbook reconciliation

**Reviewed:** 2026-10-27
**Reference:** [DecisionTrace implementation runbook](02_DECISIONTRACE_IMPLEMENTATION_RUNBOOK.md), [portfolio release evidence matrix](04_RELEASE_EVIDENCE_MATRIX.md), and the separate DecisionTrace repository at commit [`d752ac7`](https://github.com/Preethamreddy29/decisiontrace/commit/d752ac793281ca6a71ccbc291e346a570beb3079). Its [fresh-stack CI run](https://github.com/Preethamreddy29/decisiontrace/actions/runs/40386335864) passed. This is a scope and evidence assessment, not a v1 release claim.

## Assessment

The project follows the portfolio's **separate-repository and parallel standalone development** decision. Phase 0 corpus and Phase 1 design gates have evidence. A local foundation and a useful fictional v0.6 demo run in CI. Stage A outbox and concurrent revocation checks now pass, and the first Stage B full-text retrieval slice is in place. The version number is a preview identifier: it does **not** mean the runbook's `v0.5.0-alpha-mvp` deployment or Phase 4 exit gate has passed.

The implementation diverged from the full runbook by delivering a deterministic two-topic demo before the planned general retrieval/model pipeline. This made the historical decision and citation workflow demonstrable early, but leaves the central v1 retrieval, extraction, evaluation, and operations work ahead. The Phase 2 gate record explicitly covers the local core stack; the broader Phase 2 runbook items (pgvector, artifact/model adapters, stage telemetry) are not yet complete.

| Runbook phase | Evidence now | Completion status against the full runbook |
|---|---|---|
| 0 — Charter/corpus | Licensed six-month fictional seed, 14 source versions, 25 specified questions, checksum manifest | Passed seed gate; 100+ reviewed gold set is later work. |
| 1 — Design/threats | Temporal model, API/event drafts, ten ADRs, threat map | Design gate passed; contracts and threat tests must track the expanded runtime. |
| 2 — Foundation | PostgreSQL/API/worker/web Compose, checksummed migrations, seed, health and CI; authorized temporal full-text chunk search | Local core passed; pgvector, artifact storage, local model profile, full ingestion states, and telemetry remain. |
| 3 — Temporal cited answer | Valid/recorded-time controls, approved decision versions, bounded exact citations, abstention and a fictional demo | Preview works; hybrid retrieval, structured generation, verifier pipeline, independently reviewed labels, and real issuer test remain. |
| 4 — Full MVP | Markdown/transcript/JSON intake, source sections, three change-watch relation types, independent approval, source revocation | Partial; extraction review, complete decision fields/relations, full source adapters, semantic drift, dashboard, exports, and 100+ questions remain. |
| 5 — Security/failure | Server-derived tenant/role, input bounds, some isolation/revocation checks | Partial; full authorization matrix, lineage deletion/retention, adversarial set, race/failure drills, and degraded-mode guarantees remain. |
| 6 — Evaluation/observability | 25 seed prompts, 14 paraphrases, 20 agent-authored draft holdout cases, local/CI checks | Release evaluation open; independent labels, 100+ cases, pipeline comparisons, slice metrics, latency/memory and monitoring remain. |
| 7–9 — RC, v1, proof | Demo guide and preview release notes | Open; backup/restore, rollback, clean-machine RC, exact image promotion, tagged v1, case study and cost model remain. |

## Stage A reliability checkpoint

The worker now validates and acknowledges every current local event type; unknown, malformed, and future-version events dead-letter by design. A safe replay command handles known valid old dead letters, and the local outbox schema matches its runtime envelope. [Outbox CI](https://github.com/Preethamreddy29/decisiontrace/actions/runs/40367001560) and [concurrent revocation CI](https://github.com/Preethamreddy29/decisiontrace/actions/runs/40384037661) pass. `done` means local validation and acknowledgement, not external delivery. Manual UI review, a clean local stack run, and backup/restore revocation evidence remain before Stage A can be treated as fully closed.

## Build sequence and exit gates

Each stage should be a focused release candidate with a clean CI run, reproducible fixtures, measured results, and an updated progress record. Failed security or citation checks block advancement.

| Order | Build work | Exit evidence |
|---|---|---|
| A. Stabilize v0.6 | Complete outbox event handling/replay, resolve schema/runtime differences, test manual UI flows and revocation lineage, keep bounded demo working. | All emitted event types reach `done` or an intentionally documented retry/dead-letter state; no unsupported current event type; old demo suite still passes. |
| B. Complete pipeline foundation | Add PostgreSQL full-text + pgvector with tenant/permission filters, source/artifact storage abstraction, model/config version registry, pinned local embedding/reranking profile, stage telemetry, resumable ingestion states. | Fresh setup, idempotent ingest, compatible index rebuild, model checksum, per-stage traces/metrics, and no unauthorized candidate exposure. |
| C. Deliver the planned answer pipeline | Build keyword/vector fusion, reranking, temporal context, structured local generation, deterministic claim/citation verifier, and explicit abstention/failure behavior. Keep the current resolver as a measured baseline. | 25 seed questions plus reviewed cases pass; every claim opens exact authorized evidence; unsupported or model-invented citations are rejected. Record keyword/vector/hybrid comparisons and resource use. |
| D. Complete governed MVP breadth | Implement adapters for transcript, PRD, ticket, ADR, test, release and metric sources; candidate claim/decision extraction and correction queue; scope, owner, approver, assumptions, expiry, revisit triggers; all required typed relations. | Each source type ingests/version-corrects; reviewer can correct extracted candidates before approval; tenant/role checks cover source, claim, relation, review and export paths. |
| E. Add evidence-grounded drift and health | Scan approved decisions against active downstream artifacts, add contradiction rules and persisted findings with both exact evidence sides; surface assumption expiry, missing approver/outcome evidence, unresolved conflict and drift age. | Seeded true/false drift cases produce reviewable findings; new versions and revocation update findings; reviewers can resolve without rewriting evidence. Report drift precision/recall. |
| F. Harden and evaluate | Build an independently reviewed 100+ question set across the runbook slices; threat and failure drills; real OIDC issuer/browser flow; permission, citation, temporal, abstention, injection, latency and memory reports. | All hard gates in the runbook and evidence matrix pass on frozen fixtures; no tenant leak, unsupported citation, or deleted-source retrieval. Report slice failures, not only totals. |
| G. Release v1 and proof | Freeze schemas/models/index/config and manifests; test prior-tag migration, backup/restore/reindex, rollback, clean-machine install, SBOM/license review, tagged RC, exact-image v1 promotion, case study and economics. | RC and v1 signature smoke pass on named hardware; restore and rollback are rehearsed; evidence matrix links exact released artifacts. |

## Parallel inputs and dependencies

- The maintainer's independent review of `corpus/holdout_v05_draft.json` remains open. Corrections or explicit approval are needed before the bounded Phase 3 answer-quality gate can close. The 100+ question set needs separate reviewers and a frozen validation/holdout split.
- A real OIDC issuer test needs an issuer, audience, JWKS, tenant/role claim agreement, test identities, and a browser sign-in/refresh design. Synthetic signed-token tests do not close this gate.
- RuleTwin integration waits for its stable versioned evidence contract, tenant/identity semantics, fixtures, and consumer tests. DecisionTrace's standalone v1 does not need RuleTwin to complete its own core gates; an integrated demo does.
- The local model and performance targets depend on the chosen hardware. Benchmark before fixing an exact model size or delivery date. For one focused implementer, the remaining breadth is roughly **four to six months of work**, plus independent review and external integration wait. Treat this as a planning range, not a release promise.

## First next checkpoint

Finish Stage A's manual and recovery checks. Continue Stage B from the [authorized full-text chunk search](https://github.com/Preethamreddy29/decisiontrace/blob/main/docs/release/v08-full-text-foundation.md) to a pinned vector profile, compatible rebuild, and measured hybrid retrieval. Then demonstrate one end-to-end source through the versioned full-text/vector pipeline with authorized temporal retrieval (Stage B/C vertical slice). Do not mark the Phase 4 MVP or any release-matrix hard gate Passed from the current preview results.
