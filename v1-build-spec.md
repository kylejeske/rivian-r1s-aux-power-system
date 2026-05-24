# V1 Build Spec

This is the build-ready v1 specification for the Rivian R1S modular auxiliary power system. It summarizes accepted decisions and points to the canonical details.

## Architecture

- Two removable 8S LiFePO4 battery modules.
- Shared dock for module paralleling, charging, monitoring, precharge, branch distribution, and main output.
- DC-first load strategy.
- No DC-DC charging from Rivian 12V in v1.
- No inverter branch installed in v1.

## Battery Modules

- Cells: 8x EVE LF105 per module.
- Nominal module voltage: 25.6V.
- Capacity: 105Ah, about 2.69kWh per module.
- BMS: JK-B2A8S20P per module.
- Fuse: Littelfuse JLLN060 60A Class T.
- Disconnect: Blue Sea 6006, no-load service isolation only.
- Connector: gray Anderson SB120 6810G1 with 1319G6 6 AWG contacts.
- Module output wiring: 6 AWG marine-grade tinned fine-strand copper.

## Charging

- AC input: covered 15A 120VAC inlet.
- AC charger: Victron Phoenix Smart IP43 24/25.
- AC charger target: 24V, 25A, about 600W DC.
- Solar controller: Victron SmartSolar MPPT 100/30.
- Solar input: Anderson Powerpole PP45 with MC4-to-Powerpole adapter.
- Solar target: 2S portable panel setup, 200W-500W, 36V-44V Vmp, cold-corrected Voc below 75V, Isc no higher than 15A.
- Charging policy: one charging source at a time, AC or solar.

## Dock Protection and Distribution

- Dock module inputs: two Blue Sea 285-Series 60A DC breakers.
- Precharge: per-input 25 ohm 50W resistor, 2A fuse, momentary switch, and voltage test points.
- Positive busbar: covered 250A-class copper busbar.
- Negative busbar: covered 250A-class copper busbar.
- Shunt: Victron SmartShunt 500A.
- Main output fuse: Littelfuse JLLN100 100A Class T.
- Main output connector: red Anderson SB120 6810G3 with 1319 2 AWG contacts.
- Main output wiring: 2 AWG marine-grade tinned fine-strand copper.

## Loads

- Fridge: ICECO APL35 on fused 24V branch, 12 AWG, 15A fuse.
- Starlink Mini: fused native 24V branch where practical, 12 AWG, 10A fuse.
- USB-C PD: 24V-compatible 100W panel modules, fused by module rating.
- 12V accessories: Victron Orion-Tr 24/12-20 isolated converter.
- Accessory connectors: red/black Anderson Powerpole PP30/PP45 family.

## Mechanical

- Module target envelope: about 18 in W x 12 in D x 8 in H.
- Module enclosure: aluminum, 0.100 in panels minimum, 0.125 in base/end structural plates.
- Internal insulation: nonconductive liners and covered live conductors.
- Retention assumptions: 5g forward, 3g lateral, 3g vertical.
- SB120 connectors are not structural.
- Cell compression: dedicated compression frame, 0.125 in end plates, G10/fiberglass insulation, four 1/4-20 insulated rods or equivalent straps.

## Validation

- Cable fabrication must follow [Cable Fabrication Acceptance Guide](guides/cable-fabrication-acceptance.md).
- Service procedures must follow [Service Procedures](guides/service-procedures.md).
- Commissioning must follow [Commissioning Checklist](guides/commissioning-checklist.md).
- Thermal pass/fail: no termination more than 20C above comparable nearby cable under sustained load; components must stay within manufacturer ratings.

## Remaining Build Gates

- Final frunk measurements and enclosure CAD.
- Final purchased solar panel datasheet check.
- Final purchased-cell terminal torque and compression guidance check.
- Physical build, cable acceptance, commissioning, and thermal validation.

