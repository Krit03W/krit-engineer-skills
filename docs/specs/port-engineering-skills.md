# Port engineering skills from mattpocock/skills

## Goal

Bring this repo's engineering-skill coverage closer to parity with
`mattpocock/skills/skills/engineering` by porting four skills —
`improve-codebase-architecture`, `prototype`, `research`, and
`codebase-design` — adapted to this repo's own conventions, and wire them
into the main flow documentation so they're discoverable the same way
every existing skill is. Done means: a user (or Claude) can invoke or
trigger any of the four exactly as documented, on any project that has
installed this skill pack.

## Scope

**In scope:**
- `skills/improve-codebase-architecture/SKILL.md` (+ `references/` for
  the HTML report scaffold) — user-invoked, scans a codebase for
  deepening opportunities and presents them as a temp-file HTML report.
- `skills/prototype/SKILL.md` (+ `references/` for the logic-prototype
  and UI-prototype branches) — model-invoked, builds throwaway
  prototypes to answer a design question.
- `skills/research/SKILL.md` — model-invoked, delegates a research
  question to a background investigation against primary sources,
  writing cited findings to a Markdown file.
- `skills/codebase-design/SKILL.md` (+ `references/` for deepening a
  cluster and the design-it-twice pattern) — model-invoked, shared
  vocabulary for deep modules (module, interface, depth, seam, adapter,
  leverage, locality).
- Updating `README.md`'s skill table(s) and flow description so all four
  are documented alongside existing skills.
- Updating `AGENTS.md` if the new skills change any repo-wide authoring
  convention (they should not; call this out if a ticket finds otherwise).

**Out of scope:**
- `triage`, `domain-modeling`, `wizard`, `diagnosing-bugs`,
  `resolving-merge-conflicts`, `ask-matt`, `setup-matt-pocock-skills` —
  not being ported in this round.
- Any `agents/*.yaml` per-tool compat file — this repo ships plain
  `SKILL.md` files only ([ADR-0001](../adr/0001-adapt-not-port-engineering-skills.md)).
- A standalone `grilling` or `domain-modeling` skill — `grill-with-docs`
  already covers both roles ([ADR-0001](../adr/0001-adapt-not-port-engineering-skills.md)).
- Any change to the existing core flow skills
  (`grill-with-docs`, `to-spec`, `to-tickets`, `implement`, `code-review`,
  `tdd`, `wayfinder`, `work-on-issues`, `setup-krit-skills`) beyond adding
  references to the four new skills where they naturally connect.

## Approach

Port each skill's process and vocabulary content largely as-is from the
source repo (the value of, e.g., `codebase-design`'s glossary is that
exact, consistent terminology), but adapt every cross-reference so it
points at real skills in this repo instead of the source repo's:

- `improve-codebase-architecture`'s step 3 ("Grilling loop") calls the
  Skill tool with `grill-with-docs` instead of separate `grilling` /
  `domain-modeling` skills, for both the interview and the CONTEXT.md/ADR
  update side effects.
- `improve-codebase-architecture` and `codebase-design` keep referencing
  each other and `CONTEXT.md` / `docs/adr/` the same way the source does.
- Long reference material (HTML report scaffold, prototype LOGIC/UI
  branches, deepening/design-it-twice patterns) goes into each skill's
  `references/` subfolder per `AGENTS.md`'s "keep SKILL.md under ~500
  lines" rule, not inlined.
- Each `SKILL.md` frontmatter sets `name` matching its folder and a
  trigger-phrased `description`; `improve-codebase-architecture` (the
  only user-invoked one of the four) sets `disable-model-invocation:
  true`, matching how `wayfinder` and `to-tickets` are already marked in
  this repo.
- No `agents/openai.yaml` or other per-tool file is created for any of
  the four skills (see [ADR-0001](../adr/0001-adapt-not-port-engineering-skills.md)).
- README updates:
  - Add `improve-codebase-architecture` to the "Shaping: for effort too
    big to plan in one sitting" section or a new section, since like
    `wayfinder` it's a user-invoked entry point independent of the core
    flow.
  - Add `codebase-design`, `prototype`, and `research` under a new
    "Optional: design & research helpers" section, mirroring how the
    existing "Optional: AI-agent helpers" section documents
    model-invoked, independent-of-core-flow skills.

## Acceptance criteria

- [ ] `skills/improve-codebase-architecture/SKILL.md` exists, its
      frontmatter `name` is `improve-codebase-architecture`, and it sets
      `disable-model-invocation: true`.
- [ ] `skills/improve-codebase-architecture/SKILL.md` step 3 calls the
      Skill tool with `grill-with-docs`, not `grilling` or
      `domain-modeling`.
- [ ] `skills/improve-codebase-architecture` contains no `agents/`
      subfolder.
- [ ] `skills/prototype/SKILL.md` exists, frontmatter `name` is
      `prototype`, no `disable-model-invocation` field set (model-invoked
      by default).
- [ ] `skills/prototype` contains no `agents/` subfolder.
- [ ] `skills/research/SKILL.md` exists, frontmatter `name` is
      `research`, no `disable-model-invocation` field set.
- [ ] `skills/research` contains no `agents/` subfolder.
- [ ] `skills/codebase-design/SKILL.md` exists, frontmatter `name` is
      `codebase-design`, no `disable-model-invocation` field set, and its
      glossary section defines module, interface, implementation, depth,
      seam, adapter, leverage, and locality using the same definitions as
      the source skill.
- [ ] `skills/codebase-design` contains no `agents/` subfolder.
- [ ] Every one of the four `SKILL.md` files is under ~500 lines, with
      any longer reference content split into that skill's `references/`
      subfolder and linked from the `SKILL.md` body.
- [ ] `README.md` lists all four new skills in a table or section, each
      with a one-line description matching the pattern used for existing
      entries.
- [ ] `README.md`'s existing skill entries and flow diagram are otherwise
      unchanged (no accidental edits to unrelated rows).
- [ ] Each new skill has been exercised against at least one realistic
      prompt (per `AGENTS.md`: "an untested skill is a draft") and the
      test interaction is described in the ticket/PR that adds it.

## Open questions

None — resolved and confirmed with the user:

- `improve-codebase-architecture` gets its own new README section
  (targets existing codebases, not new work — distinct enough from
  `wayfinder`'s greenfield/multi-session framing to not share a section).
- The three model-invoked additions (`codebase-design`, `prototype`,
  `research`) go under a new "Optional: design & research helpers"
  section, following the existing "Optional: AI-agent helpers" section as
  a template (same structure: short intro line, then one bullet per
  skill with a one-line description, closing with a line noting they're
  independent of the core flow).

## Tickets

- [#1 — feat: add research skill for background primary-source investigation](https://github.com/Krit03W/krit-engineer-skills/issues/1)
- [#2 — feat: add codebase-design skill (deep-module vocabulary)](https://github.com/Krit03W/krit-engineer-skills/issues/2)
- [#3 — feat: add prototype skill (throwaway logic/UI prototypes)](https://github.com/Krit03W/krit-engineer-skills/issues/3)
- [#4 — feat: add improve-codebase-architecture skill (HTML deepening report)](https://github.com/Krit03W/krit-engineer-skills/issues/4)
