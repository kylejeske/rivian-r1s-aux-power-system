# Decision: Module Paralleling and Precharge

Status: accepted
Date: 2026-05-24

## Context

Modules can be paralleled only through the dock. Fuses and breakers protect faults, but they are not intended to manage normal equalization current between modules at different voltages.

## Decision

Add a current-limited precharge/equalization path for each dock module input.

Use a 25 ohm, 50W chassis resistor, 2A fuse, and momentary switch per module input. Provide voltage test points for module positive, bus positive, and common negative.

## Open Questions

- Confirm exact resistor, fuse holder, and momentary switch part numbers.
- Confirm test point style and placement in dock layout.

## Evidence

- A resistor path limits equalization current before closing the 60A dock input breaker.
- 25 ohm keeps current controlled even under accidental multi-volt mismatch.
- Momentary control prevents the precharge path from being left on unintentionally.

## Consequences

- Dock module input sequence becomes: breaker off, connect SB120, check voltage, hold precharge, confirm delta, close breaker, release precharge.
- Target voltage delta before paralleling is 0.10V or less.
- Absolute maximum voltage delta before attempting precharge is 0.20V; above that, do not parallel.
- The feature supports future multi-module expansion without relying on connector arcing or breaker closure to absorb equalization.

## Links

- Checklist section: [6. Module Paralleling and Precharge / Equalization](../build-readiness-checklist.md#6-module-paralleling-and-precharge--equalization)
- Diagram: [Precharge/equalization](../diagrams/precharge-equalization.mmd)
- Structured data: [components](../data/components.json)

