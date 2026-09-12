# Agent-Domain Questions

Read this file only when the current work involves an AI agent, RAG
pipeline, or MCP tool (per `CONTEXT.md`'s "Agent stack" line). Weave the
relevant questions below into the `grill-with-docs` interview — don't ask
ones that don't apply to this piece of work.

- **Data boundary.** What can this agent read? How fresh does it need to
  be? What happens when the source is stale or unavailable?
- **Tool boundary.** Which tools/MCP servers may it call? For each: is it
  read-only or does it have side effects (send, write, delete, spend
  money)? Side-effecting tools need explicit confirm-before-call
  behavior in the implementation — flag this for the `implement` step.
- **Guardrails.** What must this agent never do, even if asked directly?
- **What a bad answer looks like, concretely.** Push for one real
  example — "it should be accurate" is not a completion.
- **Evaluation.** Is there a golden test set? If not, note that
  `agent-eval-loop` should be run once one exists, and flag that ticket
  in `to-tickets`.
- **Fallback behavior.** What happens when the agent doesn't know, or a
  tool call fails — say so plainly, retry, escalate, or degrade silently?
  Pick one.

If the work touches RAG retrieval quality specifically, `rag-pipeline-review`
is the deeper reference for chunking/embedding/retrieval questions — this
file only covers the interview-level questions, not the technical audit.
