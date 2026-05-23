# Information Schemas

This folder contains structured schemas for design data that should stay consistent across diagrams, BOMs, tables, and checklists.

The goal is to make design decisions machine-checkable over time. For example, a wire schedule entry should reference a fuse, connector, circuit current, and diagram identifier instead of living as an isolated row in a Markdown table.

## Planned Schemas

- [x] [`decision.schema.json`](decision.schema.json) - design decision records with evidence and links.
- [x] [`component.schema.json`](component.schema.json) - reusable component records for cells, BMS, fuses, connectors, chargers, converters, and loads.
- [ ] `circuit.schema.json` - circuit definitions with voltage, current, fuse, wire, connector, and source/load relationships.
- [ ] `wire-schedule.schema.json` - conductor schedule entries.
- [ ] `fuse-table.schema.json` - fuse/protection entries.
- [ ] `connector.schema.json` - connector family, keying, color, contact, and rating records.
- [ ] `test-plan.schema.json` - commissioning and validation test definitions.

## Conventions

- Use JSON Schema draft 2020-12 unless there is a reason to choose otherwise.
- Include `$id`, `title`, `description`, `type`, and `required` fields.
- Prefer explicit units in property names, for example `currentA`, `voltageV`, `lengthFt`, `temperatureC`.
- Include references back to diagrams or checklist sections where useful.
