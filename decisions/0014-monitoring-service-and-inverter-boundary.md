# Decision: Monitoring, Service, and Future Inverter Boundary

Status: accepted
Date: 2026-05-24

## Context

The dock must be diagnosable in the field and leave a clean boundary for optional future inverter integration without expanding v1 scope.

## Decision

Use Victron SmartShunt 500A for dock monitoring. Provide labeled voltage test points, service checklists, spare fuses, and a circuit label map.

Reserve inverter space only in v1. Do not install an inverter connector, fuse, or energized branch.

## Open Questions

- Confirm final label artwork after physical layout.
- Confirm whether future inverter target exceeds 100A before adding any inverter hardware.

## Evidence

- SmartShunt placement has already been defined on the negative side.
- A future inverter could exceed the v1 100A dock target, so it needs a separate design review.

## Consequences

- SmartShunt settings: 105Ah for one module, 210Ah for two modules, charged voltage 28.0V, tail current 4%, Peukert 1.05.
- Field service includes pre-departure, install, removal, charging, and fault isolation checklists.
- Future inverter branch must remain shunt-measured and separately fused if added later.
- V1 carries a label: "INVERTER RESERVED - NOT ENERGIZED IN V1".

## Links

- Checklist section: [13. Monitoring, Diagnostics, and Service Procedures](../build-readiness-checklist.md#13-monitoring-diagnostics-and-service-procedures)
- Checklist section: [14. Future Inverter Integration](../build-readiness-checklist.md#14-future-inverter-integration)
- Guide: [Service procedures](../guides/service-procedures.md)

