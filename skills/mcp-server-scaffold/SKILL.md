---
name: mcp-server-scaffold
description: Scaffold a new MCP (Model Context Protocol) server following consistent naming, schema, and error-handling conventions. Use when starting a new MCP tool or server for an agent, or when the user asks to expose an internal API/database/service to an agent via MCP.
---

# MCP Server Scaffold

## Steps

1. **Purpose.** Ask what this server exposes (one sentence) and list the
   tools it will provide as verb_noun names (e.g. `search_files`,
   `create_ticket`) — not noun-only names (`files`, `ticket`).

2. **Transport.** Ask stdio (local, single-user) or HTTP/SSE (shared,
   multi-user, needs auth). Default to stdio for personal/local tools.

3. **Per-tool contract.** For every tool, require before writing code:
   - Explicit input schema (types, required vs optional fields)
   - Explicit error envelope — what does a failure response look like,
     and does it distinguish "bad input" from "upstream service down"?
   - Idempotency note — is calling it twice with the same input safe?
     Side-effecting tools (write/delete/send) must say so in the
     description so the calling agent treats them with the right caution.

4. **Read-only vs side-effecting split.** Group tools into read-only and
   side-effecting. Side-effecting tools get a `[side-effecting]` marker in
   their description so any orchestrating agent knows to confirm before
   calling.

5. **Generate the skeleton.** Use FastMCP (Python) or the project's
   existing MCP scaffolding if one exists — check `CONTEXT.md`'s "## Agent
   Stack" section first. Wire each tool to a stub that returns a
   not-implemented error, not a silent no-op.

6. **Smoke test.** Run the server locally and confirm `list_tools`
   returns every tool with its schema before writing any real logic.

**Completion criterion:** `list_tools` returns the full tool list with
schemas and no tool is missing an error-envelope description or an
idempotency note.
