# Decision: Charging Input Paths

Status: accepted
Date: 2026-05-23

## Context

The build needs practical charging without adding unnecessary vehicle integration. The Rivian has a 1500W max 120VAC inverter output, while the 12V accessory outlet is limited to 180W.

The 12V outlet is too small for meaningful charging. The 120VAC outlet is large enough for a moderate AC charger.

## Decision

Use two v1 charging paths:

- 120VAC input feeding a Victron Phoenix Smart IP43 24/25 AC charger.
- Solar input feeding a Victron SmartSolar MPPT 100/30.

Use a covered 15A 120VAC inlet for shore/Rivian AC input. Use an Anderson Powerpole PP45 solar input on the dock, with an MC4-to-Powerpole adapter cable for panels.

Target solar around 200W to 500W portable, with a preferred 2S panel configuration: roughly 36V to 44V Vmp, cold-corrected Voc below 75V, and Isc no higher than 15A at the dock input.

Skip DC-DC charging in v1.

## Open Questions

- Confirm exact AC inlet part number.
- Confirm exact portable solar panels before final PV fuse/breaker sizing.
- Confirm final charger settings after BMS model/settings are selected.

## Evidence

- 24V x 25A is about 600W DC output.
- One 25.6V 105Ah module is about 2.69kWh, so 600W charging is roughly 5 to 5.5 hours from empty.
- Two modules are roughly 5.38kWh, so 600W charging is roughly 10 to 11 hours from empty.
- Rivian 12V accessory outlet at 180W is not useful as a primary charging path.
- Victron Phoenix Smart IP43 24/25 supports 120-240VAC input and 24V/25A output.
- Victron SmartSolar MPPT 100/30 supports 24V batteries, 100V max PV input, and 30A max battery charge current.
- Solar input should go through the MPPT, not the AC charger or DC-DC charger.

## Consequences

- No Orion XS or other DC-DC charger in v1.
- AC charger sizing stays comfortably below the Rivian 1500W inverter limit.
- Solar panels with MC4 leads need an adapter harness to the dock's Anderson Powerpole solar input.
- Final PV fuse/breaker sizing waits until the exact panel Isc and string count are known.

## Links

- Checklist section: [1. Charger Selection and Charge Architecture](../build-readiness-checklist.md#1-charger-selection-and-charge-architecture)
- Diagram: [Charging input architecture](../diagrams/charging-input-architecture.mmd)
- Structured data: [components](../data/components.json)
