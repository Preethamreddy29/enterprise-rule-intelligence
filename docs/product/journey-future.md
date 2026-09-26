# RuleTwin Future Journey

1. The analyst creates a tenant-scoped candidate from a validated declarative schema; code execution is impossible.
2. The service resolves compatible dependencies and effective dates, then rejects invalid scope before replay.
3. The analyst selects a seeded dataset manifest and exact baseline/candidate versions.
4. The API records an idempotent simulation request and outbox event in one database transaction.
5. An isolated worker replays each event deterministically, persists checksummed results, and can resume safely after failure.
6. A versioned deterministic risk policy compares tenant-specific impact and fails closed when evidence/policy is missing or invalid.
7. QA/release reviewers inspect the result, coverage, policy reasons, and provenance; approval binds to the exact checksum and policy version.
8. An auditor reproduces the result tuple later without changing a production system.

The future workflow is a design target, not implemented behavior. UI authorization is not a substitute for server-side tenant and role checks.