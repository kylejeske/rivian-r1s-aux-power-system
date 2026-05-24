# Decision: Thermal Design and Validation

Status: accepted
Date: 2026-05-24

## Context

The system runs in a vehicle frunk with limited airflow and vibration. Thermal validation must prove that the conservative electrical design remains cool in the actual enclosure.

## Decision

Use passive cooling for v1 with aluminum mounting plates for heat-producing electronics. Validate with staged load and charge tests using an IR camera and contact thermocouples.

## Open Questions

- Confirm final temperature limits against any purchased-component manuals that are stricter than this baseline.

## Evidence

- Heat risk is concentrated at terminations, fuses, breakers, BMS, charger, MPPT, DC converter, and busbars.
- Actual enclosure testing is stronger evidence than ampacity tables alone.

## Consequences

- Worst-case design ambient: 50C frunk air.
- Pass/fail: no connector/lug/fuse/breaker more than 20C above nearby cable under sustained load, and no component above manufacturer rating.
- BMS MOS temperature must remain below 70C during sustained 50A module testing.
- Charger/MPPT/DC converter mount to aluminum heat-spreader plates with air gap around them.
- Any hot termination is remade before field use.

## Links

- Checklist section: [11. Thermal Design and Validation](../build-readiness-checklist.md#11-thermal-design-and-validation)
- Guide: [Commissioning checklist](../guides/commissioning-checklist.md)

