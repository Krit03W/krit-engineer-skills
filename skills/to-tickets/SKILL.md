---
name: to-tickets
description: Split a confirmed spec into small, independently-buildable tickets using vertical slices, and create them as real GitHub (or GitLab/local) issues linked back to the spec. Use once a spec from to-spec is confirmed and ready to become actual tracked work items — this is the skill that actually files the issues, not just a plan for doing so.
---

# To Tickets

Turns a confirmed spec into real tracked issues — not a markdown list
that lives only in the chat. Read `CONTEXT.md`'s "## Engineering Setup"
section first for the tracker, repo, and labels (run `setup-krit-skills`
if missing).

## Steps

1. **Slice the spec into vertical slices.** Each ticket should deliver a
   thin, independently-testable piece of end-to-end behavior — not a
   horizontal layer ("write the DB schema" as its own ticket with no
   working behavior attached). A good test: could this ticket ship alone
   and demonstrably work? If not, it's too thin or badly cut.

2. **Draft each ticket** with:
   - Title: `feat: <specific, concrete outcome>` (or `fix:`/`chore:` as
     appropriate)
   - Body: which acceptance criteria from the spec this covers (quote
     them), plus any implementation notes specific to this slice
   - A link back to the spec file (`docs/specs/<slug>.md`)

3. **Create the issues for real**, per the tracker configured in
   `CONTEXT.md`:

   **GitHub:**
   ```bash
   gh issue create --repo <owner/repo> \
     --title "feat: <title>" \
     --body "$(cat <<'EOF'
   Spec: docs/specs/<slug>.md

   Covers acceptance criteria:
   - <criterion 1>

   Notes:
   <implementation notes>
   EOF
   )" \
     --label "<label from CONTEXT.md, e.g. ready>"
   ```
   Capture the returned issue number/URL for each ticket.

   **GitLab:** same shape with `glab issue create --repo <owner/repo> ...`

   **Local markdown:** append each ticket to `docs/tickets/<slug>.md`
   with a stable local ID instead of a tracker issue number.

4. **Write a small index back into the spec file** — a "## Tickets"
   section at the bottom of `docs/specs/<slug>.md` listing each ticket
   title with its issue number/link, so the spec and its breakdown stay
   discoverable from one place.

5. **Report back** the list of created issues (numbers + titles + URLs)
   to the user — don't just say "tickets created," show what was
   actually filed so they can sanity-check the slicing before anyone
   starts building.

**Completion criterion:** every ticket exists as a real issue (or local
markdown entry) with a working link back to the spec, and the spec has a
"## Tickets" section listing all of them — not just described in chat.

## Where this leads

Each ticket is now ready for `implement` to pick up, one at a time.
