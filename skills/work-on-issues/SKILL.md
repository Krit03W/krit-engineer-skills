---
name: work-on-issues
description: Fetch ready, unblocked tickets from the issue tracker and work through them sequentially — implement, review, report — one at a time, without the user having to manually invoke implement for each one. Use when the user says "work through the backlog", "pick up the next ticket", "burn down the ready issues", or wants several tickets built in one autonomous run.
---

# Work On Issues

Sequential autopilot over `implement` + `code-review`, built to stop
rather than guess whenever a ticket isn't actually ready. Read
`CONTEXT.md`'s "## Engineering Setup" section first.

## Steps

1. **Ask the mode up front, once:** stop after each ticket for review, or
   keep going through every ready ticket unattended? Don't assume — a
   wrong assumption here means either annoying interruptions or several
   tickets built on a bad early decision before anyone notices.

2. **Fetch the queue.**
   ```bash
   gh issue list --repo <owner/repo> --label ready --state open \
     --json number,title,labels,body --jq 'sort_by(.number)'
   ```
   Skip any issue that's already assigned to someone else, or whose body
   references an unresolved `Depends on #<n>` for a ticket that's still
   open.

3. **For each ticket, in order:**
   a. Run the full `implement` skill against it (claim, branch, TDD loop,
      commit, open PR referencing `Closes #<n>`).
   b. Run `code-review` against the resulting diff.
   c. If review finds a **blocking** issue: stop the whole run, leave the
      ticket assigned and labeled accordingly (e.g. `blocked` or
      `needs-changes`), and report to the user — do not attempt to
      silently fix and re-review in a loop with no limit.
   d. If review is clean: mark the ticket `needs-review` (for a human) or
      merge-ready per the project's actual merge policy from
      `CONTEXT.md` — don't auto-merge unless the user explicitly said so
      for this run.

4. **Between tickets**, if running in "stop after each" mode: report
   status and wait. If running in "keep going" mode: move to the next
   ticket in the queue, but still stop immediately on anything genuinely
   ambiguous (a ticket whose acceptance criteria don't match what the
   code actually needs, a missing dependency, conflicting instructions)
   rather than making a judgment call that should be the user's.

5. **Final report** (end of run or on stop): list every ticket touched,
   its outcome (merged-ready / needs-review / blocked), and why, for
   anything blocked.

**Completion criterion:** every ticket the run touched has a tracker
status reflecting its real outcome, and the run stopped on the first
genuinely ambiguous or blocking situation rather than pushing through it.
