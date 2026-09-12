---
name: setup-krit-skills
description: One-time setup for the krit-engineer-skills repo in a project. Configures the issue tracker (GitHub/Linear/local), where specs and ADRs live, ticket labels, and the agent stack (if any). Run this once per repo before using grill-with-docs, to-spec, to-tickets, implement, or code-review.
disable-model-invocation: true
---

# Setup krit-engineer-skills

User-invoked, one-time setup. Writes a "## Engineering Setup" section into
`CONTEXT.md` (creating the file if needed) that every other skill in this
repo reads before doing anything else. Do not skip this.

## Steps

1. **Issue tracker.** Ask: GitHub Issues, GitLab, Linear, or local
   markdown under `docs/tickets/`? If GitHub or GitLab, ask for the
   `owner/repo` and confirm the `gh` (or `glab`) CLI is authenticated —
   run `gh auth status` and show the result rather than assuming.

2. **Labels.** Ask what labels this project uses for ticket state (e.g.
   `spec`, `ready`, `in-progress`, `blocked`, `needs-review`). If the repo
   already has labels, run `gh label list --repo <owner/repo>` and show
   them instead of asking blind. Default suggestion if none exist:
   `spec`, `ready`, `in-progress`, `needs-review`, `done`.

3. **Doc locations.** Confirm where specs (`docs/specs/`), ADRs
   (`docs/adr/`), and tickets index (if using local markdown instead of
   GitHub) should live. Create the folders if they don't exist.

4. **Agent stack** (skip if this project has no AI-agent component). Ask:
   orchestration framework (LangGraph/LangChain/n8n/none), RAG store
   (pgvector/ChromaDB/Qdrant/none), MCP servers involved. This only feeds
   `rag-pipeline-review`, `mcp-server-scaffold`, and `agent-eval-loop` —
   skip entirely for a non-agent project.

5. **Write `CONTEXT.md`:**

   ```markdown
   ## Engineering Setup
   - Tracker: <GitHub/GitLab/Linear/local> — repo: <owner/repo or n/a>
   - Labels: <list>
   - Specs: docs/specs/  |  ADRs: docs/adr/
   - Agent stack: <orchestration> / <RAG store> / <MCP servers> (or "n/a — not an agent project")
   ```

**Completion criterion:** `CONTEXT.md` has a filled-in "## Engineering
Setup" section with no literal placeholder left, and if GitHub/GitLab was
chosen, `gh auth status` (or `glab auth status`) has been confirmed
working — not just assumed.
