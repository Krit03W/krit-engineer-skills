---
name: to-spec
description: Turn an agreed conversation (from grill-with-docs) into a written spec document, without re-interviewing the user. Use once grill-with-docs has settled what to build and the user is ready to move from talking to a written plan — synthesize what was already discussed, don't ask new questions.
---

# To Spec

No interview here — this skill only synthesizes what's already been
agreed in the conversation (typically via `grill-with-docs`) into a
written artifact. If something critical is still ambiguous, that's a
sign `grill-with-docs` wasn't finished — go back to it rather than
guessing here.

## Steps

1. **Draft the spec** at `docs/specs/<slug>.md` with these sections:
   - **Goal** — one paragraph, what "done" looks like
   - **Scope** — what's in, what's explicitly out
   - **Approach** — the agreed design, referencing any ADRs from
     `grill-with-docs`
   - **Acceptance criteria** — a checklist an agent (or a human) can use
     to verify the work is actually finished, each item concrete and
     checkable
   - **Open questions** — anything genuinely still unresolved; don't
     hide these to make the spec look more finished than it is

2. **Cross-check against `CONTEXT.md`** — use the project's established
   vocabulary, don't reintroduce looser phrasing.

3. **Show the draft to the user** and ask for confirmation before
   treating it as settled.

**Completion criterion:** the spec file exists, every acceptance
criterion is phrased as a checkable statement (not "works well" but "call
returns X for input Y"), and the user has confirmed it — not just
received it silently.

## Where this leads

Hand off to `to-tickets` to slice the confirmed spec into buildable work.
