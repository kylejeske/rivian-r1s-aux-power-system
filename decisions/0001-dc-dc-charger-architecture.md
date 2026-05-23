# Decision: DC-DC Charger Architecture

Status: accepted-with-open-source-current-question
Date: 2026-05-23

## Context

The dock needs controlled DC-DC charging for an 8S/24V LiFePO4 bank. The original design named "Victron Orion XS" generically, but the Orion XS models are not interchangeable.

## Decision

Use the Victron Orion XS 1400 for mixed-voltage DC-DC charging into the 8S/24V battery bank.

Do not use the Orion XS 12/12-50A for this bank; its output range is too low for 8S LiFePO4.

Default to charger mode. Do not use fixed-voltage power-supply mode unless a later decision explicitly justifies it.

## Open Questions

- What exact source feeds the charger: Rivian 12V, external DC, or something else?
- What continuous input current is safe from that source?
- How is charge enable/disable controlled: remote on/off, service switch, BMS allow-to-charge, or source-voltage detection?
- What final charge settings coordinate with the selected BMS?

## Evidence

- Orion XS 1400: 9V-35V input, 10V-35V output.
- Orion XS 12/12-50A: 10V-17V output, so reject for 24V bank.
- Orion XS 1400 installation guidance: 60-70A external battery protection, 6 AWG under 5m or 4 AWG for 5-10m, vertical mounting, cooling clearance, and strain relief.
- Rivian 12V source-current limit remains unverified.

## Consequences

- Charger model choice is resolved.
- Charger input fuse/wire sizing remains blocked by source-current verification.
- Provisional output current target: 20A single-module, 30A-40A dual-module, pending BMS and thermal validation.

## Links

- Checklist section: [1. Charger Selection and Charge Architecture](../build-readiness-checklist.md#1-charger-selection-and-charge-architecture)
- Diagram: [DC-DC charger architecture](../diagrams/dc-dc-charger-architecture.mmd)
- Structured data: [components](../data/components.json)
