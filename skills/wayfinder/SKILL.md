---
name: wayfinder
description: Chart an effort too big for one session as a map of decision tickets on the issue tracker, then resolve them one at a time until only implementation remains. Use for a greenfield project, a build spanning many sessions, or when the route to the destination is still genuinely foggy — not for a single well-scoped feature (use grill-with-docs for that instead).
---

# Wayfinder

Plans, does not build. A wayfinder ticket holds a *question* whose
resolution is a decision — never a slice of the product to implement.
That distinction is the rule agents break most often with this skill:
watch for it constantly.

Read `CONTEXT.md`'s "## Engineering Setup" section first.

## When to actually reach for this

Ask: could the whole thing be settled in one sitting? If yes, use
`grill-with-docs` instead — it's cheaper and this skill is genuinely
slower and denser. Only proceed here if the effort spans multiple
sessions and the route to the destination isn't clear yet. Say this
check out loud to the user before starting; if the answer turns out to
be "small," stop and hand off to `grill-with-docs`.

## Steps

1. **Name the destination.** What does reaching the end of this map look
   like — a spec ready to hand off, a locked decision, a proof of
   concept, a completed migration? Fix this before any ticket exists; it
   is what every ticket gets measured against. Confirm it with the user
   explicitly.

2. **Create the map** as one issue labeled `wayfinder:map`, with four
   sections:
   - **Destination** — from step 1
   - **Decisions so far** — empty at first; one line per closed ticket
     later, each linking to where the real detail lives
   - **Not yet specified** — the fog of war: decisions you can tell are
     coming but can't phrase precisely yet
   - **Out of scope** — work ruled beyond the destination (closed, never
     graduates into a ticket)

3. **Chart the first cut of tickets.** Breadth-first: what's the first
   layer of things that need deciding? For each, open a child issue
   labeled `wayfinder:<type>` — see `references/ticket-types.md` for the
   four types (`grilling`, `prototype`, `research`, `task`) and which to
   pick. If this pass turns up no real fog at all, stop here and tell the
   user the effort is small enough to skip the map entirely.

4. **Resolve tickets from the frontier** — the open, unblocked,
   unclaimed tickets. One ticket per session by default (exception:
   `research` tickets can run in parallel with others). Claim a ticket by
   assigning it to yourself before working it. When resolved: post the
   answer as a resolution comment, close it, add one line to the map's
   **Decisions so far**, and check whether resolving it makes anything in
   **Not yet specified** concrete enough to graduate into a fresh ticket.

5. **Prototype aggressively, don't planmax.** Where uncertainty can be
   flushed out with a cheap throwaway artifact instead of more talking,
   do that — a map scoped to one bounded destination behaves far better
   than one that tries to plan an entire product. If the map grows past
   ~15-20 tickets before implementation starts, that's a signal to narrow
   the destination, not to keep charting.

6. **When the map clears** (frontier empty, fog empty): hand off to
   `to-spec` on the map issue to collapse the linked decisions into one
   spec, then `to-tickets` to slice that into real implementation work.
   **Do not go straight to `implement`** — the map is a set of decisions,
   not a build plan, and skipping the collapse throws away the linked
   detail. Only skip straight to implementation if, in hindsight, the
   whole effort turned out small enough that the two extra steps aren't
   worth it — say so plainly if that's the call being made.

## Known failure modes to watch for

- **Scope creep inside the map's own Notes.** The "plan, don't build"
  default can only be overridden by editing the map — and the map is
  written by the same agent the rule constrains. Read the Notes on any
  map you didn't chart yourself before assuming execution is authorized.
- **A `task` ticket quietly becomes a build ticket.** If it reads like a
  piece of the destination rather than something that unblocks a
  decision, it's mistyped — flag it, don't just build it.
- **Late tickets resting on assumptions early ones invalidated.** Keep
  the destination bounded (one epic, not "build the whole product") and
  prototype early to catch this before it compounds.
- **A decision that closed turns out wrong later.** Don't quietly design
  around it — tell the user what changed; update the map, revise
  affected tickets, and comment on the closed one rather than leaving it
  looking still-valid.

**Completion criterion:** the destination was written and confirmed
before the first ticket existed, every currently-open ticket reads as a
question (not "build the X"), **Not yet specified** has been shrinking
over time rather than growing, and the session that clears the map hands
off to `to-spec` — it does not open a pull request.
