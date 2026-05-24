# Decision: Dock Busbar, Shunt, and Main Output

Status: accepted
Date: 2026-05-24

## Context

The dock combines two protected module inputs, charging sources, branch loads, monitoring, and the main high-current output.

## Decision

Use covered 250A-class positive and negative busbars, a Victron SmartShunt 500A, a 100A Class T main output fuse, and an Anderson SB120 main output wired with 2 AWG fine-strand copper.

Reserve physical space for a future inverter takeoff, but do not install the inverter fuse/takeoff in v1.

## Open Questions

- Confirm exact covered busbar part numbers after stud count and dock layout are drawn.
- Confirm exact SB120 housing color/key for the main output.

## Evidence

- 250A busbars provide margin over the 100A dock target.
- SmartShunt 500A has ample range for the 100A dock and future monitoring margin.
- 100A Class T output protection matches the combined dock output target.
- 2 AWG main output cable reduces voltage drop and heat versus smaller conductors.

## Consequences

- Main output path becomes: positive busbar -> 100A Class T fuse -> SB120 main output positive.
- Negative path must route module negatives through the battery side of the SmartShunt and all loads/chargers through the system side.
- Future inverter support remains a layout reservation, not an installed energized branch.

## Links

- Checklist section: [5. Dock Input Protection and Bus Architecture](../build-readiness-checklist.md#5-dock-input-protection-and-bus-architecture)
- Structured data: [components](../data/components.json)

