# Account-aware MCP Multiplexer

A standalone MCP gateway that routes requests to account-scoped upstream MCP connections while enforcing tenant isolation and per-account authorization.

## Status

Project foundation. Implementation is intentionally developed on feature branches with pull requests targeting .

## Design goals

- Isolate credentials, sessions, tools, and resources by account.
- Route MCP initialization and subsequent requests to the correct account context.
- Prevent cross-account tool discovery and invocation.
- Support explicit account selection and well-defined default-account behavior.
- Preserve upstream MCP protocol semantics and provide auditable request correlation.
- Keep secrets out of logs, URLs, and persisted diagnostic output.

## Development

See [ARCHITECTURE.md](ARCHITECTURE.md) for the initial system boundaries and [ROADMAP.md](ROADMAP.md) for proposed feature slices.
