---
name: code-review
description: Review a diff or pull request against both the linked spec's acceptance criteria and general code-design standards (deep modules, single responsibility, no dead code). Use whenever the user asks to review a diff, a PR, or code someone (or an agent) just wrote, or before merging any ticket built by implement.
---

# Code Review

Reviews against two things, not one: does it satisfy the spec, and is it
well-designed regardless of the spec. A change can pass every acceptance
criterion and still be bad code — call that out too.

## Steps

1. **Get the diff.** `gh pr diff <n>` if there's a PR, or `git diff` /
   `git diff main...HEAD` otherwise.

2. **Check against the spec.** Open the linked `docs/specs/<slug>.md` and
   the specific ticket's claimed acceptance criteria. For each: does the
   diff actually satisfy it? Point to the specific lines, don't take the
   ticket's word for it.

3. **Check code design**, independent of the spec:
   - Are modules deep (small interface, real behavior behind it) or is
     this a shallow pass-through that adds indirection without value?
   - Any duplicated logic that should be a single source of truth?
   - Dead code, commented-out blocks, or debug logging left in?
   - Do names match the project's vocabulary in `CONTEXT.md`, or did new
     ad-hoc terminology sneak in?
   - Test quality: do the tests verify real behavior, or just re-assert
     whatever the implementation happens to do?

4. **Classify findings** as blocking (must fix before merge) vs.
   suggestion (worth a follow-up ticket, not worth blocking on). Don't
   let nitpicks block a change that meets the spec and is well-designed.

5. **Leave the review** — `gh pr review <n> --comment/--request-changes/--approve`
   with the findings, or post inline if no PR system is in use.

**Completion criterion:** every acceptance criterion has an explicit
verified/not-verified verdict tied to specific lines, and every blocking
finding is distinguished from suggestions — not one undifferentiated
list of comments.
