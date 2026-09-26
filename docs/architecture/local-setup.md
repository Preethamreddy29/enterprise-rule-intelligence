# Local Setup

## Current Phase 0

This repository is documentation-only. No Python or Node environment, Docker services, database, or application command exists yet. You can read/edit the Markdown and inspect Git without installing dependencies. Do not copy `.env.example` to a local secret file: it is intentionally configuration-free at this phase.

## Planned RuleTwin development environment (Phase 2; not yet verified)

Prerequisites from the handbook: Git 2.4x+, Docker Desktop/Engine with Compose v2, Python 3.12 with `uv` or Poetry and Ruff, Node.js 22 LTS with `pnpm`, PostgreSQL 16 (normally through Compose), and Make or an equivalent task runner. The planned application stack is local Docker Compose with API, web, worker, PostgreSQL; observability is optional. No paid services, cloud database, or public backend.

Exact commands, versions, ports, health/readiness behavior, migration/seed commands, and `.env` variables must be documented and verified during Phase 2 before this page can claim a working setup. The project should provide one documented clean-clone startup/check sequence at that gate.

## Configuration and secrets

- Configuration will be environment-based and schema-validated at service startup.
- `.env.example` will contain variable names and safe non-secret examples only after owners/defaults are specified.
- Never commit credentials, tokens, passwords, private keys, tenant data, database files, model files, or generated artifacts.
- Local secrets remain outside version control; no external API key is required by the zero-cost target.
