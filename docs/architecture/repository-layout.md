# Repository Layout and Topology

## Current checkout

The `main` branch contains the supplied execution sources as the portfolio baseline. The Phase 0 branch contains portfolio/RuleTwin planning artifacts only. The maintainer confirmed on 2026-09-27 that this checkout is the portfolio index and planning repository; retain the supplied sources and do not place product runtime here.

## Portfolio standards

The engineering handbook and blueprint call for four repositories: this portfolio index plus separate RuleTwin, DecisionTrace, and BoundaryOps repositories. No monorepo will be created. ADR-001 records the accepted boundary. Product runtime, product-owned contracts, tests, databases, and deployment evidence belong in their respective repositories.

## Portfolio index contents

```text
.
├── .env.example
├── README.md
└── docs/
    ├── 00_PORTFOLIO_ENGINEERING_HANDBOOK.md   # supplied; preserve
    ├── 01_RULETWIN_IMPLEMENTATION_RUNBOOK.md # supplied; preserve
    ├── 02_DECISIONTRACE_IMPLEMENTATION_RUNBOOK.md # supplied; preserve
    ├── 03_BOUNDARYOPS_IMPLEMENTATION_RUNBOOK.md   # supplied; preserve
    ├── 04_RELEASE_EVIDENCE_MATRIX.md          # supplied; preserve
    ├── 05_GITHUB_WORKFLOW_TEMPLATES.md        # supplied; preserve
    ├── Technical_Product_Portfolio_Project_Blueprint.md # supplied context; preserve
    ├── README.md                              # supplied; preserve
    ├── architecture/                          # system context, topology, setup, tests
    ├── decisions/                             # ADRs and explicit unresolved decisions
    ├── product/                               # RuleTwin Phase 0 product evidence
    ├── security/                              # threat model
    ├── operations/                            # progress and known limitations
    ├── release/                               # evidence index/status
    ├── implementation-plan.md
    └── requirements-traceability.md
```

## Future separate RuleTwin repository

```text
ruletwin/
├── .github/                    # CI, templates, dependency and security controls
├── apps/api/                   # FastAPI transport
├── apps/worker/                # outbox consumer and simulation execution
├── apps/web/                   # React + TypeScript + Vite
├── packages/domain/            # pure deterministic rules, policies, aggregates
├── packages/contracts/         # OpenAPI, JSON Schema, generated/validated types
├── packages/test_support/      # deterministic fixtures and test factories
├── db/migrations/              # immutable PostgreSQL migrations
├── db/seeds/                   # fixed-seed synthetic NovaBill data
├── docs/                       # product, architecture, data, security, ops, ADRs
├── evals/                      # fixtures, expected results, versioned reports
├── infra/compose/              # local core and optional observability profiles
├── scripts/                    # clean bootstrap, seed, checks, evidence helpers
├── tests/{unit,integration,contract,security,performance,e2e}/
├── .env.example
├── docker-compose.yml
└── README.md
```

Omit unused components; no AI/model service or managed queue is needed for RuleTwin. This layout does not authorize code creation in this checkout. Creating/configuring the separate repository and any GitHub action require explicit approval. Separate DecisionTrace and BoundaryOps repositories/databases remain future work, each independently deployable.
