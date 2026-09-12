# 0001. Adapt, don't verbatim-port, borrowed engineering skills

## Context

We're bringing 4 skills from `mattpocock/skills/skills/engineering` into this
repo: `improve-codebase-architecture`, `prototype`, `research`, and
`codebase-design`. Two things in the source material don't have an
equivalent here:

- `improve-codebase-architecture` calls out to separate `grilling` and
  `domain-modeling` skills for the CONTEXT.md/ADR update loop. This repo
  has no such skills — `grill-with-docs` already does both the interview
  and the CONTEXT.md/ADR maintenance in one skill.
- Every source skill ships an `agents/openai.yaml` file for Codex
  compatibility. No skill in this repo has a per-tool compat file; our own
  README states these are "plain `SKILL.md` files — no lock-in."

## Decision

Adapt the 4 ported skills to this repo's actual conventions instead of
copying them verbatim:

- Wherever a source skill would call `grilling` or `domain-modeling`, call
  `grill-with-docs` instead.
- Do not create `agents/*.yaml` compat files for any ported skill.
- Keep the source material's domain vocabulary and process structure
  otherwise intact (e.g. `codebase-design`'s deep-module glossary is the
  point of the skill — that content is preserved as-is).

## Consequences

- Ported skills are consistent with every other skill already in this
  repo, rather than introducing a second, parallel set of conventions.
- If a future skill genuinely needs a standalone grilling or
  domain-modeling loop independent of `grill-with-docs`, that's a new
  decision to make then — this ADR doesn't rule it out, it just says the
  current 4-skill port doesn't need it.
- Anyone comparing this repo to the upstream `mattpocock/skills` source
  will see fewer files per skill (no `agents/` folder) and fewer total
  skills (no separate `grilling`/`domain-modeling`) — expected, not a gap.
