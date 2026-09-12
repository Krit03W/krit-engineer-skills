# Wayfinder Ticket Types

Every ticket on a wayfinder map carries a `wayfinder:<type>` label and is
either **HITL** (resolved through a live exchange with the user) or
**AFK** (the agent alone can resolve it).

| Type | Mode | Reach for it when | Resolved by |
|---|---|---|---|
| `grilling` | HITL | The default — the question can be settled by talking it through. | Run `grill-with-docs`'s interview discipline in a fresh session, then record the answer as a resolution comment and close. |
| `prototype` | HITL | "How should this look/behave" — a question talking cannot settle. | Build a small throwaway artifact, link it from the ticket as an asset, let the user choose — never pick for them and close it yourself. |
| `research` | AFK | A fact outside this codebase is blocking a decision. | A research pass (web search / doc lookup) run in parallel with other tickets — the only ticket type that can run concurrently with others safely. |
| `task` | Either | Nothing to *decide*, but manual work blocks a decision — provisioning access, signing up for a service, moving data so its shape can be seen. | The agent alone where possible, otherwise a precise checklist for the human. **Never** a slice of the actual product build — that's the single most common way this ticket type goes wrong. |

## Rule of thumb

If a ticket's title could be rewritten as "build the X," it's mistyped —
either it belongs downstream of the map (as an implementation ticket from
`to-tickets`, after the map clears), or it needs to be reframed as an
actual open question.
