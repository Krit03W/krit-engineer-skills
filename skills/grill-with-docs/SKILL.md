---
name: grill-with-docs
description: Interview the user about a plan or feature before any code is written, and use the answers to build/sharpen the project's shared vocabulary in CONTEXT.md and ADRs. Use every time before starting new work — a new feature, a new project, or any change where "what exactly are we building" hasn't been nailed down yet in this conversation.
---

# Grill With Docs

The core planning skill. Almost every real bug traces back to
misalignment between what the user meant and what the agent built. This
skill closes that gap *before* code exists, and pays it forward by
sharpening the project's shared language so future sessions need fewer
words to say the same thing.

Read `CONTEXT.md` first (run `setup-krit-skills` if it doesn't exist yet).

## Steps

1. **Interview, one question at a time.** Do not dump a list of questions
   at once — ask, wait for the answer, ask the next one. Cover, at
   minimum:
   - What does "done" look like for this piece of work, concretely?
   - What existing code/modules does this touch or depend on?
   - What's explicitly out of scope for this round?
   - Is there a real example of the input/output, or the before/after?
   - Any deadline, performance, or compatibility constraint?

   If this is an AI-agent, RAG, or MCP-related project (check
   `CONTEXT.md`'s "Agent stack" line), also read
   `references/agent-domain-questions.md` and weave in the relevant
   questions from there — data boundary, tool boundary, guardrails,
   evaluation criteria. Skip that file entirely for non-agent work.

2. **Listen for jargon.** Whenever the user or the codebase uses a
   domain term loosely ("the materialization thing", "when a course goes
   live"), stop and pin it down: what's the precise name for this
   concept? Record it.

3. **Update `CONTEXT.md`.** Add or revise a glossary entry for any term
   sharpened in step 2. The goal: a later session (or a different agent)
   reads one line and understands the concept, instead of re-deriving it
   from scratch.

4. **Record hard-to-explain decisions as ADRs.** For any non-obvious
   choice made during the interview (why this approach and not the
   obvious alternative), write a short ADR to `docs/adr/<next-number>-<slug>.md`:
   Context / Decision / Consequences. Link it from `CONTEXT.md`.

5. **Summarize back to the user** what was agreed, in the sharpened
   vocabulary from step 3, and confirm before moving on.

**Completion criterion:** the user has explicitly confirmed the summary
in step 5, `CONTEXT.md` reflects any new/changed terms, and every
question in step 1 has a real answer or an explicit "not applicable" —
not a silently skipped one.

## Where this leads

Small, single-session work → go straight to `implement`.
Larger, multi-step work → hand off to `to-spec` next.
