# Roadmap

Each capability is developed in its own branch/worktree and pull request targeting . Feature PRs should be independently reviewable and merged in dependency order.

1. **Core runtime** — protocol server, configuration, lifecycle, health, and graceful shutdown.
2. **Account model and storage** — account records, encrypted credential references, ownership, and revocation.
3. **Identity and policy** — caller authentication, account discovery, authorization, and deny-by-default checks.
4. **Upstream connection manager** — account-scoped connection pools, concurrency bounds, retries, and cleanup.
5. **MCP routing** — initialize, tools/list, tools/call, resources, prompts, and notifications with session affinity.
6. **Catalog isolation** — account-qualified names, deterministic collision handling, and per-account caching/invalidation.
7. **Operations and audit** — redacted logs, metrics, tracing, administrative APIs, and operational documentation.
8. **Hardening** — threat model, cross-account isolation tests, load tests, and deployment guidance.

## Acceptance baseline

Every feature must include tests for the happy path, invalid inputs, authorization failures, session lifecycle, and cross-account isolation where relevant. No feature may rely on frontend filtering as a security boundary.
