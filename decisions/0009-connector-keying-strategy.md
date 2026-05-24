# Decision: Connector Keying Strategy

Status: accepted
Date: 2026-05-24

## Context

The system has removable battery modules, a main high-current output, solar input, regulated accessory outputs, and service connections. Connector keying should prevent unsafe cross-connection.

## Decision

Use gray Anderson SB120 connectors for battery module-to-dock inputs:

- Gray SB120 housing: 6810G1.
- 6 AWG silver contact: 1319G6.

Use red Anderson SB120 for the main 24V high-current output:

- Red SB120 housing: 6810G3.
- 2 AWG silver contact: 1319.

Reserve blue Anderson SB175 for a future inverter path, but do not install it in v1.

Use Anderson Powerpole PP45 for solar input with an MC4-to-Powerpole adapter cable. Use red/black Powerpole connectors for regulated DC accessory outputs.

Use SB120 environmental boots with covers on exposed/removable SB120 connectors:

- SB120 source boot with cover: 3-6034P1.
- SB120 load boot with cover: 3-6035P1.

Use Deutsch DTM 4-pin connectors for low-current BMS display/service wiring unless the final JK harness requires a different pin count.

## Open Questions

- Confirm exact low-current accessory connector panel parts after load layout.
- Confirm final BMS display/service pinout against the JK harness.

## Evidence

- Different SB housing colors are mechanically keyed and reduce unsafe cross-mating.
- Anderson SB120 datasheet lists 6810G1 gray housing, 6810G3 red housing, 1319G6 6 AWG contact, and 1319 2 AWG contact.
- Anderson SB120 environmental boots provide IP64 protection with covers.
- Keeping solar on Powerpole avoids confusing PV input with SB120 battery connectors.
- Reserving SB175 for inverter use keeps future high-current expansion distinct from the 100A v1 output.

## Consequences

- Gray SB120 means battery module input only.
- Red SB120 means main 24V high-current output only.
- Solar and accessory Powerpole ports require clear voltage/function labels.
- BMS service/display wiring gets a dedicated low-current keyed connector.
- Future inverter support remains physically and electrically distinct.

## Links

- Checklist section: [8. Connector Strategy](../build-readiness-checklist.md#8-connector-strategy)
- Structured data: [components](../data/components.json)
