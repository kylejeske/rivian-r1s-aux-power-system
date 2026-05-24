# Decision: Load Distribution and Accessories

Status: accepted
Date: 2026-05-24

## Context

Primary loads are fridge, Starlink Mini, USB-C PD, lighting, and small electronics. The build should remain DC-first and avoid designing around large inverter loads.

## Decision

Use a fused 24V branch block for native 24V loads and a Victron Orion-Tr 24/12-20 isolated converter for regulated 12V accessories.

Run Starlink Mini from a fused native 24V output where practical. Use panel-mount 24V-compatible USB-C PD modules for USB-C charging. Use red/black Powerpole outputs for regulated DC accessories.

## Open Questions

- Confirm exact USB-C PD module part numbers.
- Confirm exact panel output count after dock layout.
- Confirm final ICECO and Starlink cable terminations when cables are purchased.

## Evidence

- Starlink Mini supports 12-48VDC and 100W USB PD guidance; 24V is a better DC source than long 12V wiring.
- ICECO APL35 is a low-power fridge load suitable for fused DC distribution.
- Isolated 24V-to-12V conversion keeps accessory 12V loads regulated and separate from the 24V bus.

## Consequences

- Fridge branch: 24V fused output, 12 AWG, 15A fuse.
- Starlink branch: 24V fused output, 12 AWG, 10A fuse.
- USB-C PD branch: fused 24V input to PD modules, 12 AWG feed, fuse by module rating.
- 12V accessory converter: Victron Orion-Tr 24/12-20 isolated, input fused at 15A, output fused at 25A max.
- Lighting/small electronics stay on branch fuses sized to actual loads.

## Links

- Checklist section: [12. Load Distribution and Accessory Outputs](../build-readiness-checklist.md#12-load-distribution-and-accessory-outputs)

