# Design Decisions

This folder contains design decision records for choices that affect safety, compatibility, serviceability, cost, or future expansion.

Use one decision per file once a topic is resolved or intentionally deferred. The checklist remains the project control surface; decision records provide the evidence behind checked-off items.

## Planned Decision Records

- [ ] DC-DC charger model and charge architecture.
- [ ] MPPT and solar input architecture.
- [ ] JK BMS model and configuration.
- [ ] Module fuse and disconnect selection.
- [ ] Dock-side module input protection.
- [ ] Module paralleling and precharge/equalization.
- [ ] Connector color/keying strategy.
- [ ] Mechanical sled retention strategy.
- [ ] Thermal validation acceptance limits.
- [ ] Future inverter boundary.

## Template

```markdown
# Decision: Short Title

Status: proposed | accepted | rejected | superseded
Date: YYYY-MM-DD

## Context

What problem or uncertainty this decision resolves.

## Decision

The chosen approach.

## Evidence

Datasheets, calculations, tests, or constraints that support the decision.

## Consequences

Tradeoffs, limitations, and follow-up work.

## Links

- Checklist section:
- Diagrams:
- Schemas/data:
```

