# Decision: Mechanical Enclosure and Retention

Status: accepted
Date: 2026-05-24

## Context

The battery sleds and dock live in the Rivian frunk. They must be removable, serviceable, vibration-resistant, and mechanically retained independent of electrical connectors.

## Decision

Use aluminum battery module enclosures with nonconductive internal liners and covered live conductors. Use a rigid dock tray with guided rails, positive latches, and secondary retention.

Design retention assumptions: 5g forward, 3g lateral, and 3g vertical. SB120 connectors are alignment/current paths only, not structural retention.

## Open Questions

- Confirm final enclosure CAD and fastener pattern.
- Confirm exact latch/rail hardware after frunk measurement.

## Evidence

- Aluminum gives rigidity, heat spreading, and practical fabrication.
- Nonconductive liners reduce enclosure short risk.
- Vehicle hard-braking and vibration require mechanical restraint independent of connector friction.

## Consequences

- Module enclosure target remains about 18 in W x 12 in D x 8 in H.
- Use 0.100 in aluminum minimum for enclosure panels and 0.125 in aluminum for base/end structural plates.
- Add two handles per module and a service panel for fuse/BMS/disconnect access.
- Use neoprene/EPDM isolation pads, but constrain the module so it cannot bounce or fret connectors.

## Links

- Checklist section: [9. Mechanical Enclosure and Sled Retention](../build-readiness-checklist.md#9-mechanical-enclosure-and-sled-retention)
- Diagram: [module physical layout](../diagrams/module-physical-layout.mmd)
- Diagram: [dock physical layout](../diagrams/dock-physical-layout.mmd)

