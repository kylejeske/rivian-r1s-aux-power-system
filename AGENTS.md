# AGENTS

Guidance for agents working in this repository.

## Project Control Documents

- Treat `build-readiness-checklist.md` as the primary control document.
- When a design choice is made, update the checklist first.
- If a choice affects wiring, layout, component selection, validation, service procedure, or safety, add or update the relevant artifact in `diagrams/`, `schemas/`, `data/`, or `decisions/`.
- Link checklist items back to the decision, diagram, schema, or data file that closes them.

## Decision Records

Decision records in `decisions/` must stay compact and skimmable.

Use this structure:

- Context
- Decision
- Open Questions
- Evidence
- Consequences
- Links

Keep decision records concise. Do not turn them into long engineering memos. Put detailed tables, calculations, schemas, component data, or diagrams in dedicated files and link to them from the decision record.

## Repo Style

- Prefer Markdown for human-facing design notes.
- Prefer Mermaid source files for diagrams.
- Prefer JSON Schema and JSON for reusable structured design data.
- Keep safety-critical assumptions explicit.
- Do not mark checklist items closed unless the supporting evidence is linked.

