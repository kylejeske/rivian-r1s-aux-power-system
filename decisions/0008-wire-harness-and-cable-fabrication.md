# Decision: Wire Harness and Cable Fabrication

Status: accepted
Date: 2026-05-24

## Context

The system uses removable modules, high-current dock wiring, AC charging, solar input, and branch loads. Cable quality affects safety, voltage drop, heat, vibration resistance, and serviceability.

## Decision

Use marine-grade tinned fine-strand copper cable with 105C insulation where practical.

Build v1 cables in-house using proper crimp tooling, adhesive heat shrink, labeling, continuity checks, pull checks, and visual inspection.

## Open Questions

- Confirm exact lug, heat-shrink, and SB contact part numbers.
- Confirm final cable lengths after physical layout.

## Evidence

- Fine-strand tinned copper cable is appropriate for vibration-prone mobile/marine-style DC systems.
- In-house cable fabrication is acceptable if every cable passes a documented acceptance process.

## Consequences

- Main dock output uses 2 AWG.
- Module output and dock input paths use 6 AWG.
- AC charger DC output, MPPT battery output, and branch fuse block feed use 8 AWG unless a final manual/layout check permits otherwise.
- Solar input adapter uses 10 AWG PV wire.
- Accessory outputs default to 12 AWG, with 14 AWG only for light loads.
- No cable goes into final assembly unless it passes the cable fabrication acceptance guide.

## Links

- Checklist section: [7. Wire, Lug, Crimp, and Harness Specification](../build-readiness-checklist.md#7-wire-lug-crimp-and-harness-specification)
- Guide: [Cable fabrication acceptance guide](../guides/cable-fabrication-acceptance.md)
- Structured data: [components](../data/components.json)

