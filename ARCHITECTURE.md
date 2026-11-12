# Architecture

## Purpose

The multiplexer provides one MCP-facing endpoint over multiple account-specific upstream MCP connections. An account is a security boundary, not merely a routing label.

## Core concepts

- **Account**: an isolated identity and credential set for one upstream service context.
- **Upstream**: an MCP server connection owned by exactly one account.
- **Client session**: an MCP protocol session bound to one account for its lifetime unless an explicit, authenticated account-switch protocol is designed and approved.
- **Tool catalog**: the tools visible within the selected account; catalogs must never be unioned across accounts by default.
- **Policy**: authorization applied before discovery and invocation, with deny-by-default behavior.

## Request flow

1. Authenticate the caller.
2. Resolve an account from trusted identity and explicit account-selection policy.
3. Authorize the caller for that account.
4. Resolve or create an upstream MCP connection scoped to that account.
5. Forward the MCP request without leaking credentials across account boundaries.
6. Record redacted audit metadata and release resources according to session lifecycle.

## Security invariants

- No credential may be shared between accounts implicitly.
- A client session cannot change account context silently.
- Tool names and IDs are namespaced or otherwise collision-safe across accounts.
- Every invocation is re-authorized; tool visibility alone is not authorization.
- Account deletion/revocation invalidates associated sessions and pooled connections.
- Logs exclude bearer tokens, API keys, cookies, and credential-bearing URLs.

## Initial deployment shape

Start as a single service with explicit interfaces for identity resolution, account storage, policy evaluation, upstream connection management, and MCP transport. Keep persistence and transport adapters replaceable. Avoid distributed components until measured requirements justify them.

## Open design questions

- Which identity provider and account model should be first-class?
- Should the first upstream adapter support Streamable HTTP only, or also stdio and SSE?
- Is account selection per endpoint, per client session, or per request? The default should be session-bound after authenticated selection.
- How should multiple upstream tool catalogs handle name collisions: account-qualified names, aliases, or both?
- Which audit retention and administrative controls are required?
