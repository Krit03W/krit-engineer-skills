# AGENTS.md

This repo is a skill pack, not an application. If you are an agent working
*inside* this repo (editing the skills themselves):

- Each skill lives at `skills/<skill-name>/SKILL.md`. The folder name
  must exactly match the `name:` field in that file's YAML frontmatter.
- Keep `SKILL.md` bodies under ~500 lines. Push long reference material
  into a `references/` subfolder and point to it from the SKILL.md body
  instead of inlining it.
- Every skill needs a `description` field written to trigger reliably:
  state both what it does and when to use it, using phrasing a model
  would actually match against ("use whenever the user...").
- User-invoked-only skills (orchestration skills meant to be typed, not
  auto-triggered) should set `disable-model-invocation: true`.
- Test a new or edited skill against a few realistic prompts before
  committing — an untested skill is a draft, not a shipped one.

If you are an agent working in a project that has *installed* skills from
this repo: read `CONTEXT.md`'s "## Engineering Setup" section first
(written by `/setup-krit-skills`) before using any other skill here. The
main flow is `grill-with-docs → to-spec → to-tickets → implement →
code-review`; don't skip straight to `implement` on multi-session work
just because it's faster.
