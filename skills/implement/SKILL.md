---
name: implement
description: Build a single ticket (from to-tickets) into working code, test-first, one vertical slice at a time. Use whenever the user asks to work on, build, or pick up a specific ticket or issue number, or says "let's implement <ticket>".
---

# Implement

Builds exactly one ticket per session by default. Read `CONTEXT.md`'s
"## Engineering Setup" section for the tracker/repo. See the `tdd` skill
for the full red-green-refactor discipline this relies on.

## Steps

1. **Claim the ticket.** If using GitHub/GitLab, assign it to yourself
   (`gh issue edit <n> --add-assignee @me`) before starting — this is
   what tells anyone else it's taken. Read the linked spec section for
   full context, not just the ticket body.

2. **Branch.** Create `ticket/<n>-<short-slug>` off the base branch.

3. **Red-green-refactor loop** (see `tdd` for detail): write a failing
   test for the smallest next piece of the ticket's acceptance criteria,
   make it pass, refactor, repeat until every acceptance criterion this
   ticket covers is met.

4. **Keep it to this ticket.** If you discover the ticket needs
   something outside its own scope, don't silently expand it — stop and
   flag it to the user, or file it as a new ticket via `to-tickets`
   rather than scope-creeping the current one.

5. **Commit** with a message referencing the ticket
   (`feat: <summary> (#<n>)`), and if there's a PR workflow, open the PR
   with `Closes #<n>` in the description so merging closes the issue
   automatically.

6. **Update the ticket's label** (e.g. `in-progress` → `needs-review`)
   once the PR is open, per the labels configured in `CONTEXT.md`.

**Completion criterion:** every acceptance criterion this ticket claims
to cover has a passing test demonstrating it, the ticket/issue reflects
the current real status (not stale), and nothing outside this ticket's
stated scope was touched without being flagged.

## Where this leads

Hand off to `code-review` before merging.
