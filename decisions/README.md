# Design Decisions

This folder contains design decision records for choices that affect safety, compatibility, serviceability, cost, or future expansion.

Use one decision per file once a topic is resolved or intentionally deferred. The checklist remains the project control surface; decision records provide the evidence behind checked-off items.

## Planned Decision Records

- [x] [DC-DC charger model and charge architecture](0001-dc-dc-charger-architecture.md) - deferred unless future DC input is added.
- [x] [Charging input paths](0002-charging-input-paths.md).
- [ ] MPPT and solar input architecture.
- [x] [JK BMS model and charge policy](0003-bms-selection-and-charge-policy.md).
- [x] [Module fuse and disconnect selection](0004-module-fuse-and-disconnect.md).
- [x] [Dock-side module input protection](0005-dock-input-protection.md).
- [x] [Dock busbar, shunt, and main output](0006-dock-busbar-shunt-main-output.md).
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
