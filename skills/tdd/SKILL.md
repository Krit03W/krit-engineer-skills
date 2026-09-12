---
name: tdd
description: The red-green-refactor discipline used by the implement skill. Model-invoked reference — consult this whenever writing code test-first, or whenever the user asks specifically about TDD, test-first workflow, or the red-green-refactor loop.
---

# TDD (Red-Green-Refactor)

One vertical slice of behavior at a time, never a batch of tests written
upfront for the whole ticket.

## The loop

1. **Red.** Write one test for the smallest next piece of behavior. Run
   it — confirm it actually fails, and fails for the expected reason
   (not a typo or import error). A test you haven't watched fail is not
   verified to test anything.
2. **Green.** Write the minimum code to make that one test pass. Resist
   adding anything the current test doesn't require yet — that belongs
   in a later cycle, driven by its own test.
3. **Refactor.** With the test passing, clean up — remove duplication,
   improve naming, deepen the module's interface if it got shallow. Rerun
   the test after every refactor step; it must stay green throughout.
4. **Repeat** until every acceptance criterion in scope for this ticket
   is covered by a passing test.

## What makes a good test here

- Tests behavior visible through the module's public interface, not
  internal implementation details that would break on a harmless
  refactor.
- One logical assertion per test — a test with five unrelated assertions
  hides which one actually matters when it fails.
- Names the behavior, not the method: `returns_404_for_missing_ticket`,
  not `test_get_ticket_2`.

## What breaks this loop

- Writing implementation code before a failing test exists for it.
- Writing a test that passes on the first run — it isn't testing
  anything new; go back and find what it should have failed on first.
- Skipping the refactor step because "it works" — technical debt
  compounds fastest right here.
