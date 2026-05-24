# Decision: Connector Keying Strategy

Status: accepted
Date: 2026-05-24

## Context

The system has removable battery modules, a main high-current output, solar input, regulated accessory outputs, and service connections. Connector keying should prevent unsafe cross-connection.

## Decision

Use gray Anderson SB120 connectors for battery module-to-dock inputs.

Use red Anderson SB120 for the main 24V high-current output.

Reserve blue Anderson SB175 for a future inverter path, but do not install it in v1.

Use Anderson Powerpole PP45 for solar input with an MC4-to-Powerpole adapter cable. Use red/black Powerpole connectors for regulated DC accessory outputs.

## Open Questions

- Confirm exact SB120 contact part numbers for 6 AWG module wiring and 2 AWG main output wiring.
- Confirm exact low-current accessory connector panel parts after load layout.
- Confirm service connector style for BMS display/service wiring.

## Evidence

- Different SB housing colors are mechanically keyed and reduce unsafe cross-mating.
- Keeping solar on Powerpole avoids confusing PV input with SB120 battery connectors.
- Reserving SB175 for inverter use keeps future high-current expansion distinct from the 100A v1 output.

## Consequences

- Gray SB120 means battery module input only.
- Red SB120 means main 24V high-current output only.
- Solar and accessory Powerpole ports require clear voltage/function labels.
- Future inverter support remains physically and electrically distinct.

## Links

- Checklist section: [8. Connector Strategy](../build-readiness-checklist.md#8-connector-strategy)
- Structured data: [components](../data/components.json)

