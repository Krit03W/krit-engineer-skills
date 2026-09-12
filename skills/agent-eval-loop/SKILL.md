---
name: agent-eval-loop
description: Run or set up a red-green-refactor-style evaluation loop for an AI agent, using a golden test set and Langfuse/RAGAS, before shipping a change to a prompt, RAG config, or agent graph. Use whenever the user changes agent behavior and asks to verify it didn't regress, or wants to set up agent evals from scratch.
---

# Agent Eval Loop

This is the agent-work equivalent of TDD's red-green-refactor loop: no
prompt/RAG/graph change ships without a before/after comparison against a
golden set.

## If no golden set exists yet

1. Ask for 10-20 real (or realistic) queries the agent should handle well,
   plus what a good answer or correct tool call looks like for each.
2. Store them under `evals/<agent-name>/golden-set.jsonl` (one JSON object
   per line: `{"input": ..., "expected": ...}`).
3. This is a starting point, not a finished suite — say so to the user,
   and suggest growing it from real failures over time.

## Running the loop

1. **Baseline.** Run the current (pre-change) agent version against the
   golden set, log results to Langfuse (or the project's configured eval
   tool from `CONTEXT.md`), and record the score.
2. **Change.** Apply the prompt/RAG/graph change.
3. **Re-run.** Run the same golden set against the changed version.
4. **Compare.** Produce a table: query → baseline result → new result →
   verdict (improved / regressed / unchanged). Do not average this away
   into a single score without also showing the per-query regressions —
   an improved average can hide a new failure on a case that used to pass.
5. **Decide.** If any previously-passing case now fails, treat it as a
   blocker, not a footnote — surface it clearly and let the user decide
   whether the tradeoff is acceptable, rather than shipping silently.

**Completion criterion:** a per-query comparison table exists showing
every regression explicitly, not just a net score — and the user has
seen it before the change is considered done.
