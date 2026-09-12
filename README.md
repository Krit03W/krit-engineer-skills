# krit-engineer-skills

A standard engineering flow for shipping real products with AI coding
agents — idea to filed GitHub issues to reviewed code — instead of vibe
coding on feel. Built in the spirit of
[mattpocock/skills](https://github.com/mattpocock/skills) and
[utarn/engineer-skills](https://github.com/utarn/engineer-skills); adapted
and extended with real issue-tracker automation.

These are plain `SKILL.md` files — no lock-in, works with Claude Code,
Cursor, Codex, or Copilot. Fork it, delete what you don't need, edit the
rest.

## Quickstart

```bash
npx skills@latest add <your-github-username>/krit-engineer-skills
```

Run `/setup-krit-skills` first — every other skill reads its config.

List without installing: `npx skills@latest add <user>/krit-engineer-skills --list`
Install one skill: `npx skills@latest add <user>/krit-engineer-skills --skill to-tickets`

## The main flow (core)

This is the spine. Run these in order for any real piece of work:

```
/grill-with-docs → /to-spec → /to-tickets → /implement → /code-review
```

| Skill | Type | What it does |
|---|---|---|
| **`/setup-krit-skills`** | user | One-time repo config: tracker, repo, labels, doc paths. Run first. |
| **`/grill-with-docs`** | user | Interviews you about the work before any code exists; builds/sharpens `CONTEXT.md` (shared vocabulary) and ADRs as it goes. |
| **`/to-spec`** | user | Synthesizes the agreed conversation into a written spec at `docs/specs/<slug>.md` — no new questions, just writes down what was already decided. |
| **`/to-tickets`** | user | Slices the spec into vertical-slice tickets and **actually files them as GitHub/GitLab issues** (`gh issue create`), linked back to the spec. This is the piece that turns a plan into tracked, assignable work. |
| **`implement`** | model | Picks up one ticket, claims it, builds it test-first (red-green-refactor), commits with `Closes #<n>`. |
| **`/work-on-issues`** | user | Runs `implement` → `code-review` sequentially over every ready, unblocked ticket in the queue, stopping on the first blocking or ambiguous one — for burning down a backlog in one sitting instead of invoking `implement` ticket by ticket. |
| **`code-review`** | model | Reviews a diff/PR against both the spec's acceptance criteria and general code-design standards (deep modules, no dead code, real tests). |
| **`tdd`** | model | Reference: the red-green-refactor discipline `implement` runs on. |

Small, single-session work can skip straight from `grill-with-docs` to
`implement` — `to-spec`/`to-tickets` earn their keep on anything that
needs more than one sitting or more than one person picking it up.

## Shaping: for effort too big to plan in one sitting

- **`/wayfinder`** — for a greenfield project or a build spanning many
  sessions where the route is still foggy. Charts the effort as a map of
  **decision tickets** (not implementation tickets) on the tracker, and
  resolves them one at a time until only implementation remains — then
  hands off to `to-spec` → `to-tickets` like any other confirmed plan.
  Not for a single well-scoped feature; use `grill-with-docs` for that.

## Improving an existing codebase

- **`improve-codebase-architecture`** — scans a codebase (or a part of it
  you point at) for deepening opportunities, presents them as a visual
  HTML report, then walks whichever one you pick through
  `grill-with-docs` to shape the actual change. For codebases with
  history and friction, not new work — use `grill-with-docs` directly for
  that.

## Optional: AI-agent helpers

If the project involves an AI agent, RAG pipeline, or MCP server,
`grill-with-docs` automatically pulls in agent-specific interview
questions (data boundary, tool boundary, guardrails, eval criteria) — you
don't need a separate flow for that. These three skills are extra,
model-invoked helpers for that kind of work specifically:

- **`rag-pipeline-review`** — audits chunking/embedding/retrieval/reranking
  config against common RAG failure modes.
- **`mcp-server-scaffold`** — scaffolds a new MCP server with consistent
  tool naming, schemas, and error handling.
- **`agent-eval-loop`** — before/after comparison against a golden test
  set whenever a prompt/RAG/graph change ships, instead of shipping on
  vibes.

They're independent of the core flow — a non-agent project can ignore
all three and the main flow works the same.

## Optional: design & research helpers

Independent, model-invoked helpers Claude can reach for on its own when
the situation calls for them — no separate flow to run:

- **`research`** — delegates a research question to a background agent
  that investigates primary sources and writes cited findings to a
  Markdown file, so you can keep working while it reads.
- **`codebase-design`** — shared vocabulary for designing deep modules
  (module, interface, depth, seam, adapter, leverage, locality). Used by
  `improve-codebase-architecture` and reachable directly whenever a
  module's interface needs shaping.
- **`prototype`** — builds throwaway code to answer a design question: a
  single HTML file to sanity-check a state model, or several toggleable
  UI variations to answer "what should this look like?"

They're independent of the core flow — skip any of them you never reach
for and the main flow still works the same.

## Why the core flow exists

- **`grill-with-docs`** closes the #1 cause of bad AI-generated code:
  misalignment between what you meant and what the agent built.
- **`to-tickets`** is what stops planning from staying trapped in chat —
  work that isn't a real, assignable, trackable issue tends to get
  reinvented or forgotten by the next session.
- **`implement` + `tdd`** gives the agent a feedback loop, so "looks
  right" gets replaced by "the test proves it."
- **`code-review`** catches the failure mode where code satisfies the
  letter of the spec but is still a shallow, hard-to-change mess.

## Requirements

- `gh` CLI installed and authenticated for GitHub issue creation
  (`gh auth status`), or `glab` for GitLab. Without one authenticated,
  `to-tickets` falls back to local markdown under `docs/tickets/`.

## Contributing / forking

Each skill lives at `skills/<skill-name>/SKILL.md`; the folder name must
match the `name:` field in that file's frontmatter. See
[Anthropic's Agent Skills docs](https://docs.claude.com/en/docs/build-with-claude/agent-skills)
for the format. Test any new/edited skill against a few real prompts
before treating it as done — an untested skill is a draft.

---

MIT licensed.
