# Design Data

This folder is for structured project data that conforms to the schemas in [`../schemas`](../schemas).

Use this for data that should be reused across Markdown tables, diagrams, BOMs, and validation scripts.

## Planned Data Files

- [x] [`components.json`](components.json) - selected or candidate components.
- [ ] `circuits.json` - electrical circuit definitions; deferred until physical layout gives measured wire lengths.
- [ ] `wire-schedule.json` - conductor schedule; deferred until physical layout gives measured wire lengths.
- [ ] `fuses.json` - protection table; current v1 fuse decisions are recorded in `components.json`.
- [ ] `connectors.json` - connector and keying plan; current v1 connector decisions are recorded in `components.json`.
- [x] [`decisions.json`](decisions.json) - index of accepted decisions.
- [ ] `tests.json` - commissioning and validation test plan.
