# Decision: BMS Selection and Charge Policy

Status: accepted
Date: 2026-05-23

## Context

Each removable module needs its own BMS for an 8S LiFePO4 pack with a 50A operating target and 60A module fuse.

## Decision

Use one JK-B2A8S20P per battery module.

Set the v1 operating policy to one charging source at a time: AC charger or solar MPPT, not both intentionally together.

## Open Questions

- None for v1 baseline. Recheck after first bench test and thermal test.

## Evidence

- JK-B2A8S20P supports 4S-8S packs and fits the 8S module.
- 200A BMS hardware rating gives large thermal/current margin over the 50A module target and 60A fuse.
- AC charger is 25A and MPPT is 30A, so a one-source-at-a-time policy keeps normal charge current at or below 30A.
- EVE LF105 datasheet values: 3.65V max charge cutoff, 2.5V min discharge cutoff, 0C-55C charge, -20C-55C discharge.

## Consequences

- BMS hardware is not the normal current bottleneck.
- Initial BMS discharge over-current setting can be above the 60A fuse, around 70A-80A.
- Initial BMS charge over-current setting can be around 40A because combined AC+solar charging is not a v1 operating mode.
- Charge-source troubleshooting is simpler because only one charger is active at a time.
- Use two cell temperature sensors per module: one between center cells and one near an outside/end cell group. Treat the BMS MOS temperature separately.
- Provide a wired JK display/service port on each module. Bluetooth remains useful, but it is not the only service access path.

## V1 BMS Settings

| Setting | Value |
|---|---:|
| Cell over-voltage protect | 3.60V |
| Cell over-voltage recover | 3.45V |
| Cell under-voltage protect | 2.80V |
| Cell under-voltage recover | 3.00V |
| Pack charge voltage target | 28.0V to 28.4V |
| Discharge over-current protect | 75A |
| Charge over-current protect | 40A |
| Charge low-temp protect | 2C |
| Charge low-temp recover | 5C |
| Discharge low-temp protect | -20C |
| Discharge low-temp recover | -15C |
| Charge high-temp protect | 50C |
| Charge high-temp recover | 45C |
| Discharge high-temp protect | 55C |
| Discharge high-temp recover | 50C |
| Balance enable | enabled |
| Balance start voltage | 3.45V |
| Balance delta | 15mV |

## Links

- Checklist section: [3. Module BMS Selection and Configuration](../build-readiness-checklist.md#3-module-bms-selection-and-configuration)
- Structured data: [components](../data/components.json)
