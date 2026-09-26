# Technical Product Portfolio Project Blueprint

## Final recommendation

Build one coherent portfolio called **Decision Integrity Infrastructure for Configurable B2B SaaS**:

1. **RuleTwin** — predicts tenant-level effects of business-rule and configuration changes before release.
2. **DecisionTrace** — reconstructs why product decisions were made, what was believed at a past date, what later changed, and which delivery artifacts drifted.
3. **BoundaryOps** — investigates operational exceptions, tests remedies in RuleTwin, checks intent in DecisionTrace, and acts only inside explicit consequence-based limits.

The portfolio story is: **prevent unsafe changes, preserve organizational reasoning, and automate exception resolution without surrendering control**.

No market review can prove that nobody anywhere has built anything similar. The defensible novelty claim is narrower: this exact workflow and product composition is not a clone of a common tutorial or one public repository. Originality comes from the domain model, controls, evaluations, and product decisions—not from inventing every library.

## Page-by-page interpretation of the playbook

| Page | Requirement | What it means for this portfolio |
|---:|---|---|
| 1 | Prove technical product leadership through decisions, metrics, economics, risk, and communication. | Each project must be a defended product system, not a coding demo. |
| 2 | Use design, execution, and validation modes. | Choose the portfolio first, pass ten gates while building, then score and defend it. |
| 3 | Reach evidence Level 3–4 and answer what, why, how, alternatives, trade-off, and failure. | Every major component needs a forced decision and failure test. |
| 4 | Build three substantial projects with different centers of gravity. | RuleTwin owns enterprise systems, DecisionTrace owns RAG, and BoundaryOps owns agents and strategy. |
| 5 | Require problem depth, systems, measurement, trade-offs, evolution, business value, and defensibility. | All three have multiple roles, data, integrations, failures, security, economics, and scale changes. |
| 6 | Give each competency one deep home project. | Avoid shallow repetition across all three. |
| 7 | Start with a charter and real workflow. | Define users, measurable pain, non-goals, assumptions, and discovery evidence before architecture. |
| 8 | Define scope, NFRs, architecture, and decisions. | Each MVP has a narrow critical path, ADRs, and a traceable end-to-end request. |
| 9 | Demonstrate APIs, data lifecycle, delivery, scale, and recovery. | Contracts, ownership, retention, async behavior, CI/CD, rollback, and RTO/RPO are required. |
| 10 | Treat AI as a measurable system. | Separate corpus, retrieval, ranking, generation, tool, policy, and data failures. |
| 11 | Threat-model and connect technology to economics and strategy. | Tenant leakage, prompt injection, unsafe action, blast radius, unit cost, and build-vs-buy are first-class. |
| 12 | Enterprise project needs APIs, data, async work, RBAC, NFRs, observability, growth, and economics. | RuleTwin is deliberately non-AI; complexity comes from multitenancy, replay, approvals, and audit. |
| 13 | RAG project needs full ingestion, grounding, evaluation, operations, safety, and versioning. | DecisionTrace is temporal decision observability, not chat with documents. |
| 14 | Agent project needs tools, state, permissions, termination, oversight, threats, and strategy. | BoundaryOps uses typed tools, a state machine, budgets, previews, approval, rollback, and prohibited actions. |
| 15 | Produce charter, problem brief, NFR sheet, and ADRs. | These live in each repository and are maintained during the build. |
| 16 | Specify APIs, data lifecycle, AI evaluation, and regression gates. | Contracts and evaluation fixtures are version-controlled with code. |
| 17 | Maintain risks, costs, and executive summaries. | Each repo has a living risk register, cost model, and executive one-pager. |
| 18 | Demonstrate product, architecture, API, and data thinking. | Evidence is visible in flows, tests, contracts, and measured outcomes—not a skills list. |
| 19 | Cover delivery, reliability, analytics, economics, LLMs, and RAG. | Use local observability, load tests, retrieval experiments, and unit-cost estimates. |
| 20 | Cover LLMOps, agents, governance, safety, and leadership. | Use versioned evaluations, tool traces, adversarial tests, and audience-specific narratives. |
| 21 | Defend product, architecture, API, data, reliability, and RAG choices. | Add a project-specific defense document with measured evidence. |
| 22 | Defend agents, economics, strategy, and executive decisions. | Justify where an agent is unnecessary and what leadership decision is required. |
| 23 | Score observable evidence from 0–4. | A working UI is insufficient; primary competencies must reach at least Level 3. |
| 24 | Package a decision-driven case study for different audiences. | Create engineer, product-leader, and executive versions of the same story. |
| 25 | Implement only what makes decisions credible. | Build critical paths and evaluations; represent expensive scale with designs and load evidence. |
| 26 | Graduate only when all three are credible and defensible. | Maintain a portfolio dashboard and close evidence gaps. |
| 27 | Build, decide, measure, defend. | Repeat this cycle at every milestone. |

## Shared domain

Use a completely synthetic contract-to-cash or utility-billing domain. It naturally contains tenants, contracts, rates, usage events, invoices, exceptions, approvals, money-sensitive changes, and integrations.

Do not use employer code, data, schemas, screenshots, customer names, or confidential rules. Publish a synthetic-domain statement. The three projects may reuse the same event vocabulary and dataset but must remain separately deployable.

# Project 1 RuleTwin

## Product concept

A multi-tenant release-assurance platform that replays historical or synthetic events against current and proposed business rules, calculates customer and financial impact, maps dependent behavior, and blocks unsafe changes before production.

Feature-flag tools can observe a production rollout. RuleTwin asks a different question before deployment: **what outcomes would change for each tenant if this rule or configuration changed?**

## Users

- Product owner: understands affected customer workflows and KPIs.
- Configuration analyst: compares rule versions and dependencies.
- QA lead: selects a risk-based regression set.
- Release manager: enforces evidence-based approvals and rollback plans.
- Operations analyst: reproduces an outcome from its exact version context.

## Critical workflow

1. Create a candidate rule/configuration version.
2. Validate schema, dates, dependencies, and tenant scope.
3. Select a replay dataset and derive impacted scenarios.
4. Run baseline and candidate versions asynchronously.
5. Compare amount, state, error, latency, tenant, and scenario deltas.
6. Apply risk and approval policy.
7. Approve, reject, or narrow scope.
8. Record an immutable decision and emit a release-gate event.

## MVP

- Three tenants with different synthetic contracts.
- Five versioned rule types in validated JSON/YAML.
- Seeded account, usage, invoice, and exception generator.
- Deterministic baseline-versus-candidate replay.
- Rule dependency graph and affected-scenario selection.
- Delta report by tenant, workflow, rule, and financial effect.
- Author, reviewer, approver, and auditor roles.
- Approval thresholds and immutable audit events.
- One mocked deployment webhook.

Non-goals: a generic no-code rule builder, real billing, real payments, real customer integrations, and AI-generated business rules.

## Architecture

- React, TypeScript, and Vite.
- FastAPI modular monolith.
- PostgreSQL for tenants, rules, jobs, outcomes, approvals, and audit metadata.
- Local filesystem or MinIO for large artifacts.
- PostgreSQL outbox and worker for asynchronous replay.
- OpenTelemetry, Prometheus, and Grafana.
- Docker Compose.

At higher scale, separate the worker pool and artifact store first. Add a dedicated broker only when concurrent replay evidence justifies it.

## APIs

- `POST /tenants/{tenantId}/rule-versions`
- `GET /rule-versions/{versionId}/diff`
- `POST /replay-datasets`
- `POST /simulations`
- `GET /simulations/{simulationId}`
- `GET /simulations/{simulationId}/impact`
- `POST /simulations/{simulationId}/approvals`
- `POST /release-gates/evaluate`
- `GET /audit-events`

Specify tenant authorization, optimistic concurrency, idempotency, pagination, timeouts, retries, and error contracts.

## Data and decisions

Entities: Tenant, User, Role, RuleDefinition, RuleVersion, Dependency, ReplayDataset, BusinessEvent, Simulation, Run, Outcome, Delta, RiskPolicy, Approval, ReleaseGate, and AuditEvent.

Forced decisions:

1. Modular monolith versus microservices.
2. Synchronous versus asynchronous replay.
3. PostgreSQL outbox versus external broker.
4. Relational edges versus graph database.
5. Raw result retention versus summaries plus evidence samples.
6. Hard block versus warning-only gate.
7. Shared-schema versus database-per-tenant.
8. Custom RBAC versus external identity provider.

## Evaluation

Create at least 40 controlled changes: safe, tenant-isolated, cross-rule, date-boundary, rounding, missing-data, timeout, and deliberately dangerous.

Measure:

- Impact precision and recall.
- False-safe rate as the main guardrail.
- Replay determinism.
- P50/P95 job time and throughput.
- Queue age.
- Cross-tenant isolation.
- Reproducibility from rule, data, and engine versions.
- Time from proposal to approval.
- Reviewer override rate.

Test worker crash, duplicate requests, stale approval, rule cycles, malformed DSL, date overlap, webhook failure, and policy-service failure.

## Signature demo

Change a rounding and late-fee interaction for Tenant A. The system finds an effective-date cohort crossing an approval threshold, shows Tenant B is unaffected, exposes downstream exception-rule impact, blocks release, and reproduces the result from an immutable version tuple.

# Project 2 DecisionTrace

## Product concept

An evidence-first temporal RAG product that reconstructs decisions from meetings, PRDs, tickets, ADRs, tests, and releases; distinguishes changed beliefs from corrected records; detects supersession and contradiction; and finds implementation drift with claim-level citations.

The core object is a **decision contract**, not a document:

- decision, scope, owner, and approver;
- evidence and assumptions;
- valid time and recorded time;
- expiry/revisit condition;
- supersedes, contradicts, implements, tests, and measures links;
- status and implementation/outcome evidence.

## Link to the existing Meeting AI project

Reuse transcription, diarization, speaker identification, structured summaries, and local-model experience. The learning jump is from meeting intelligence to multi-source, temporally correct decision observability.

## MVP data

- Meeting transcripts.
- PRD versions.
- Ticket history exported as JSON.
- ADR and test-case markdown.
- Release notes and a synthetic metrics file.
- A six-month synthetic history containing contradictions, supersessions, corrections, stale assumptions, and drift.

## Critical workflow

1. Ingest a versioned source with checksum, permissions, timestamps, and lineage.
2. Parse sections, claims, decisions, assumptions, actions, and references.
3. Link evidence to decision contracts with confidence and human-review state.
4. Store typed relationships and create hybrid-search indexes.
5. Apply time, tenant, role, product, and artifact filters before generation.
6. Rerank evidence and construct provenance-aware context.
7. Answer with claim citations, uncertainty, conflicts, and abstention.
8. Deterministically verify cited IDs, dates, and relationship claims.
9. Compare active decisions against tickets, tests, releases, and metrics for drift.

## Architecture

- FastAPI modular monolith.
- PostgreSQL, `pgvector`, and PostgreSQL full-text search.
- Typed relational edge tables; do not add Neo4j without traversal evidence.
- Local sentence-transformer embeddings.
- Local cross-encoder reranking.
- Ollama and an existing small quantized model.
- Background ingestion and evaluation runners.
- Per-stage OpenTelemetry metrics and traces.

## Experiments

Compare fixed versus structure-aware chunks; vector, keyword, and hybrid retrieval; top-K values; pre- versus post-retrieval filters; reranking; current-state versus temporal retrieval; answer-only versus claim-citation output; and generator-only versus deterministic verification.

## Evaluation

Build at least 100 questions across factual retrieval, rationale, valid-at-date, recorded-at-date, supersession versus correction, contradiction, abstention, drift, permission denial, and injected instructions.

Measure:

- Recall@K and mean reciprocal rank.
- Temporal answer accuracy.
- Citation precision and coverage.
- Supported-claim rate.
- Contradiction precision/recall.
- Drift precision/recall.
- Abstention accuracy.
- Human usefulness with a fixed rubric.
- P50/P95 latency and memory.
- Model, retrieval, and reranking time.

Permissions must apply before retrieval. Retrieved text is untrusted. Deletion must remove retrievable chunks and invalidate derived links according to a lineage policy.

## Signature demo

Ask: “Why was manual override allowed for Tenant A on 10 May, and is it still approved?” The system reconstructs the evidence valid then, distinguishes a later correction from a policy change, shows the superseding approval, identifies a test still encoding the old behavior, and refuses to invent an unrecorded reason.

## Differentiation test

Do not build this project unless it includes all of these:

- product-specific decision contracts;
- valid-time and recorded-time semantics;
- supersession versus correction;
- claim-level verification and abstention;
- downstream implementation-drift detection;
- temporal-correctness evaluation;
- decision-health metrics such as stale assumptions and unverified outcomes.

Without them it becomes a common RAG demo.

# Project 3 BoundaryOps

## Product concept

A bounded-autonomy product-operations agent that investigates a cross-system business exception, verifies evidence, tests candidate remedies in RuleTwin, checks approved intent in DecisionTrace, and performs only reversible actions allowed by policy.

## MVP exception types

- Missing or late upstream event.
- Duplicate event/request.
- Outcome differs from deterministic replay.
- Rule effective-date conflict.
- Approved decision differs from active configuration.
- Retryable integration timeout.

## Typed tools

- `get_case`
- `get_tenant_context`
- `get_event_history`
- `get_active_rule_versions`
- `query_decision_evidence`
- `run_candidate_replay`
- `create_case_note`
- `prepare_config_patch`
- `request_approval`
- `retry_sandbox_integration`
- `rollback_sandbox_action`
- `escalate_case`

Every tool needs a schema, permission, timeout, retry rule, idempotency behavior, audit event, and mocked implementation. Treat tool output as untrusted.

## Autonomy policy

| Level | Behavior | Example |
|---:|---|---|
| 0 | Assist | Summarize evidence and missing facts. |
| 1 | Recommend | Propose a remedy for human choice. |
| 2 | Confirm then act | Prepare a reversible sandbox patch and request approval. |
| 3 | Bounded autonomy | Retry one pre-approved idempotent sandbox integration. |
| 4 | Prohibited | Never change production rules, money, data, access, or external communications autonomously. |

Confidence and consequence must be independent. High model confidence never overrides a high-consequence action.

## Control loop

1. Validate tenant, user authority, and maximum consequence.
2. Start from a deterministic investigation plan.
3. Let the model choose read-only evidence tools only where observed state changes the next step.
4. Validate every call against schema, permission, tenant, budget, and policy.
5. Persist state and evidence after every step.
6. Require RuleTwin proof for behavior-changing patches.
7. Require DecisionTrace evidence when approved intent matters.
8. Preview action, affected entities, unresolved uncertainty, and rollback.
9. Execute, request approval, or escalate.
10. Verify postconditions and roll back the permitted sandbox action if verification fails.

Use an explicit state machine. Deterministic code owns permissions, budgets, termination, action validation, and postconditions.

## Termination rules

- Maximum 12 tool calls.
- No more than two equivalent calls to the same tool.
- One retry only for explicit retryable errors.
- Stop when evidence remains unavailable.
- Stop on tenant conflict, permission failure, policy ambiguity, or prohibited action.
- Escalate when remedies have similar evidence but materially different risk.
- Track local tokens and elapsed time despite ₹0 API spend.

## Evaluation

Create at least 80 normal, ambiguous, unsafe, adversarial, and infrastructure-failure cases.

Measure task success, root-cause accuracy, correct tools, valid arguments, evidence completeness, unsafe-action prevention, escalation precision/recall, preview accuracy, rollback, termination, median steps, reviewer correction, and cross-tenant leakage.

Test indirect prompt injection, poisoned tool output, forged tenant identity, replayed approval, oversized results, stale rules, hidden duplicates, contradictory evidence, fake urgency, and attempts to invoke prohibited tools. Unsafe-action prevention should be 100% on the evaluation set.

## Signature demo

An exception says an invoice is wrong. The agent discovers an integration delay and rule mismatch, retrieves historical intent, tests two remedies in RuleTwin, rejects a document instruction to bypass approval, prepares a reversible sandbox patch, shows impact and rollback, and requests approval. A separate low-risk case allows one idempotent sandbox retry and verifies the result.

## Defensible strategy

Do not position it as a generic incident or invoice-dispute agent. Its wedge is a **proof-before-action control plane for configurable product behavior**:

- tenant-specific rules, not only alerts;
- deterministic replay required before behavior changes;
- temporally valid intent required before interpreting historical text;
- authority based on consequence, reversibility, scope, and evidence completeness;
- every action simulated, previewed, audited, and verified.

# Why the three projects belong together

| Question | RuleTwin | DecisionTrace | BoundaryOps |
|---|---|---|---|
| What will this change do? | Deterministic impact | Supplies approved intent | Requires proof before action |
| Why does behavior exist? | Shows active rule | Reconstructs rationale | Checks whether intent is proven |
| Can the system act? | Offers sandbox evidence | Supplies temporal evidence | Enforces permission and rollback |
| Principal risk | False-safe result or tenant leakage | Unsupported/temporally wrong answer | Unsafe action or cascading failure |
| Primary skill | Enterprise systems | Production RAG | Agentic AI and strategy |

Build in this order. BoundaryOps must consume stable APIs rather than copy logic from the first two products.

# Current-market boundary

Adjacent products already exist:

- LaunchDarkly provides guarded/progressive rollouts from production metrics.
- Atlassian Rovo searches work systems, extracts decisions, and connects meeting outcomes to Jira.
- PagerDuty provides AI-driven incident investigation and remediation.
- SAP presents AI assistance for financial dispute workflows.
- Open-source work explores temporal RAG, decision graphs, bitemporal stores, and durable agents.

Therefore, do not claim that feature flags, decision search, temporal RAG, agents, or approval workflows are new. Claim the specific thesis: **a governed decision-integrity layer where actions affecting configurable B2B behavior require deterministic consequence evidence and temporally valid product intent**.

# Strict ₹0 stack

| Capability | Choice |
|---|---|
| Frontend | React, TypeScript, Vite |
| Backend | Python, FastAPI |
| Data | PostgreSQL |
| Vector retrieval | pgvector |
| Keyword retrieval | PostgreSQL full-text or small BM25 library |
| Embeddings | local sentence-transformers |
| Reranking | local cross-encoder |
| LLM | existing Ollama and small quantized model |
| Async | PostgreSQL outbox and worker |
| Artifacts | filesystem or MinIO |
| Auth | local JWT and RBAC for MVP |
| Observability | OpenTelemetry, Prometheus, Grafana |
| Load testing | k6 or Locust |
| Packaging | Docker Compose |
| CI | GitHub Actions within public-repo free allowance, or local CI scripts |
| Case-study hosting | GitHub Pages |
| Data | seeded synthetic generator and hand-authored fixtures |

Do not require paid model APIs, Pinecone, managed Kafka, a cloud database, paid observability, a permanent public backend, Kubernetes, employer data, or purchased datasets.

Cash spend can remain **₹0**. Laptop RAM, disk, electricity, and time still count as costs and should be recorded. Run services sequentially and use small quantized models when necessary.

# Repository evidence

Use a portfolio index and one repository per project. Each project should contain:

- charter;
- problem brief and discovery notes;
- PRD-lite and non-goals;
- NFR sheet;
- architecture and sequence flow;
- OpenAPI specification;
- data design;
- ADRs;
- evaluation plan and fixtures;
- threat model;
- risk register;
- cost model;
- roadmap;
- executive one-pager;
- defense answers;
- source, tests, synthetic data, observability, and reproducible demo scripts.

The README should lead with the problem, measured synthetic benchmark, architecture, three decisions, failure behavior, and reproduction steps—not a wall of technology logos.

# Suggested 24-week sequence at 8–10 hours per week

| Weeks | Outcome |
|---:|---|
| 1–2 | Discovery, synthetic domain, shared vocabulary, charters, success measures |
| 3–8 | RuleTwin working slice, failures, evaluation, and case study |
| 9–14 | DecisionTrace ingestion, temporal retrieval, verification, evaluation, and case study |
| 15–20 | BoundaryOps state machine, tools, policies, adversarial evaluation, and case study |
| 21–22 | Load/security review, economics, roadmap, and scorecards |
| 23–24 | Demo recordings, portfolio page, audience narratives, and mock defenses |

Do not build all three simultaneously.

# Graduation criteria

A project is complete only when:

- The critical workflow runs on a clean machine.
- Synthetic data and evaluation commands are reproducible.
- Primary competencies score at least 3.
- Five major decisions score 4 and name revisit triggers.
- No tenant-isolation, privacy, security, or unsafe-action item remains below 2.
- Locally measurable quality, latency, reliability, and cost are measured.
- Scale claims are labeled tested, simulated, estimated, or designed.
- You can explain it in 60 seconds, five minutes, and a 30-minute defense.
- The case study states limitations and never presents synthetic outcomes as customer results.

# Final interview positioning

> I designed a three-part decision-integrity platform for configurable B2B software. RuleTwin predicts the consequences of rule changes before release. DecisionTrace reconstructs the temporally valid evidence behind product behavior and detects implementation drift. BoundaryOps uses both as controlled tools to investigate exceptions and act only within explicit, reversible limits. I measured failure, retrieval quality, latency, cost, and unsafe-action prevention, and documented what would change at enterprise scale.

## Market references

- [LaunchDarkly guarded rollouts](https://launchdarkly.com/docs/home/releases/guarded-rollouts)
- [Atlassian Rovo agents](https://support.atlassian.com/rovo/docs/atlassian-agents/)
- [Atlassian meeting decisions linked to Jira](https://jirareleases.atlassian.com/announcements/your-meeting-decisions-already-updated-in-jira)
- [PagerDuty AI for operations](https://www.pagerduty.com/ai/)
- [SAP accounts receivable AI](https://www.sap.com/use-cases/joule-assistant/accounts-receivable-ai)
- [Temporal durable execution](https://temporal.io/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

