# Rivian R1S Modular Auxiliary Power System Build-Readiness Checklist

This checklist is the working gate for turning the modular auxiliary power-system concept into a buildable design. Treat unchecked items as unresolved engineering work, not paperwork.

Status key:

- `[ ]` Open
- `[~]` In progress / partially decided
- `[x]` Closed with evidence
- `[!]` Blocking before build

## 0. Design Baseline

- [x] Architecture baseline: removable 8S LiFePO4 modules, shared dock, DC-first loads, optional external inverter.
- [x] Module baseline: 8x EVE LF105 cells, 8S, 25.6V nominal, 105Ah, JK Smart BMS, 60A module fuse, manual disconnect, SB120 output.
- [x] Current targets: 50A single-module max, 100A dual-module combined max.
- [x] No daisy chaining between modules.
- [~] Create project documentation folders for diagrams, schemas, structured data, and decisions.
- [ ] Record final system block diagram revision in [`diagrams/`](diagrams/).
- [ ] Record final per-module wiring schematic revision in [`diagrams/`](diagrams/).
- [ ] Record final dock/controller schematic revision in [`diagrams/`](diagrams/).
- [ ] Record final physical layout drawing revision in [`diagrams/`](diagrams/).
- [ ] Define reusable information schemas in [`schemas/`](schemas/).
- [ ] Store reusable design data in [`data/`](data/).
- [ ] Record accepted design decisions in [`decisions/`](decisions/).

Acceptance criteria:

- One canonical schematic set exists and matches the BOM, wiring table, fuse table, and assembly sequence.
- Checklist items that close safety-critical decisions link to their diagram, schema/data entry, or decision record.

## 1. Charger Selection and Charge Architecture

- [x] Identify intended charging paths: 120V shore power, Rivian 120V outlet, and solar input. See [D-0002](decisions/0002-charging-input-paths.md).
- [x] Defer DC-DC charging unless a future 12V/24V DC source is intentionally added. See [D-0001](decisions/0001-dc-dc-charger-architecture.md).
- [x] Define AC charger output class: 24V 25A target, roughly 600W DC output.
- [x] Select exact AC-to-24V LiFePO4 charger model: Victron Phoenix Smart IP43 24/25.
- [~] Define AC input method: covered 15A 120VAC inlet, 14 AWG internal AC wiring, hot-side 10A protection, equipment ground to metal enclosure if used, upstream GFCI assumed.
- [x] Confirm AC charger draw stays within Rivian 120V outlet limit and shore-power assumptions. 24V 25A target is comfortably below Rivian 1500W inverter limit.
- [x] Define AC charger DC output current for one-module and two-module operation: same 25A charger target for either one or two modules.
- [~] Add AC charger-specific fuse sizes to fuse table: 10A AC hot-side protection; DC output protection final after charger manual and dock conductor length review.
- [~] Add AC charger-specific wire sizes to wire table: 14 AWG AC input wiring; DC output wiring/fuse pending final dock layout.
- [~] Add AC charger mounting requirements to dock physical layout: vertical serviceable mounting, airflow around charger, AC strain relief, AC/DC separation.
- [ ] Define absorption voltage, float voltage, re-bulk behavior, and charge termination behavior.
- [ ] Define low-temperature charge cutoff strategy.
- [ ] Define behavior when BMS disconnects during charging.
- [ ] Confirm whether charger requires direct battery sense or can tolerate dock-side switching.

Acceptance criteria:

- Exact AC charger SKU is chosen.
- Its datasheet/manual explicitly supports the planned input and output voltages.
- Charge settings are written down before hardware is purchased.
- Failure behavior is understood for BMS disconnect, charger fault, source undervoltage, and module removal.

## 2. Solar / MPPT Architecture

- [x] Select exact Victron SmartSolar MPPT model: SmartSolar MPPT 100/30.
- [~] Define solar panel count, panel Voc, Vmp, Isc, and Imp. Target: portable 2S array, 200W-500W nominal, 36V-44V Vmp, cold-corrected Voc below 75V, Isc no higher than 15A at dock input.
- [ ] Calculate cold-weather corrected Voc.
- [~] Confirm PV string voltage never exceeds MPPT input limit. Target leaves margin below 100V controller limit.
- [x] Confirm PV operating voltage is high enough for a 24V battery bank: 2S portable-panel target keeps Vmp above battery voltage.
- [x] Decide whether panels are series, parallel, or series-parallel: prefer 2S portable-panel configuration.
- [~] Define PV disconnect location: dock-side solar input disconnect or breaker between solar connector and MPPT.
- [ ] Define PV fuse/breaker needs, especially if using parallel strings.
- [ ] Define MPPT battery-side fuse size from Victron manual.
- [ ] Define MPPT battery-side wire gauge and run length.
- [ ] Define temperature sense strategy for MPPT charging.
- [ ] Define what happens when modules are removed while solar is connected.

Acceptance criteria:

- PV design is valid at lowest expected ambient temperature.
- MPPT battery-side fuse and wire sizes match the selected controller manual.
- There is a safe service sequence for solar disconnect before battery/module removal.

## 3. Module BMS Selection and Configuration

- [x] Select exact JK BMS model and current rating: JK-B2A8S20P, 200A class. See [D-0003](decisions/0003-bms-selection-and-charge-policy.md).
- [x] Confirm BMS supports 8S LiFePO4.
- [x] Confirm continuous discharge current rating exceeds 60A fuse and 50A operating target with margin.
- [x] Confirm charge current rating exceeds planned charger current. V1 operating policy is one charging source at a time, so normal charge current is 25A AC or up to 30A solar.
- [ ] Confirm BMS thermal behavior inside the planned enclosure.
- [x] Define cell over-voltage cutoff and recovery: 3.60V protect, 3.45V recover.
- [x] Define cell under-voltage cutoff and recovery: 2.80V protect, 3.00V recover.
- [x] Define pack over-current cutoff and delay baseline: 75A discharge OCP, 40A charge OCP; delay TBD in commissioning.
- [x] Define charge low-temperature cutoff: 2C protect, 5C recover.
- [x] Define discharge low-temperature cutoff: -20C protect, -15C recover.
- [x] Define high-temperature charge/discharge cutoffs: charge 50C protect/45C recover; discharge 55C protect/50C recover.
- [x] Define active balancing start voltage and delta threshold: start at 3.45V/cell, 15mV delta.
- [x] Confirm number and placement of temperature sensors: two cell sensors per module, center-cell group and outside/end-cell group; BMS MOS temperature monitored separately.
- [x] Decide whether BMS Bluetooth access is sufficient or if service access is needed: provide wired JK display/service port plus Bluetooth.

Acceptance criteria:

- Exact BMS settings are recorded.
- BMS limits coordinate with charger settings instead of fighting them.
- BMS is not the only planned protection for normal charger control.

## 4. Module Fuse, Disconnect, and Fault Protection

- [x] Select exact 60A module fuse type and holder: Littelfuse JLLN060 Class T fuse with LFT30060 holder family. See [D-0004](decisions/0004-module-fuse-and-disconnect.md).
- [x] Confirm module fuse DC voltage rating and interrupt rating are adequate for 8S LiFePO4 fault current: 160VDC, 20kA DC interrupt rating.
- [x] Decide Class T vs MRBF vs other module fuse format: Class T selected for high interrupt margin.
- [~] Confirm fuse can be mounted close enough to pack positive: required; final location to confirm in module enclosure layout.
- [x] Select exact manual disconnect: Blue Sea 6006 m-Series battery switch.
- [x] Confirm disconnect is DC-rated for pack voltage and current: 48VDC max, 300A continuous.
- [x] Confirm disconnect can break expected load current without damage: treat as no-load service isolator only; do not use for normal load breaking.
- [x] Define module service sequence: turn off loads and chargers, verify near-zero current, open disconnect, then unplug SB120.
- [~] Define module fuse replacement access: required without unpacking cell stack; final panel access to confirm in enclosure layout.
- [~] Add insulated covers for fuse, disconnect, and pack positive path: required; exact boots/covers to confirm in enclosure layout.

Acceptance criteria:

- The first conductor leaving pack positive is protected as close to the cell stack as practical.
- Fuse and disconnect ratings are documented by datasheet, not inferred from current alone.

## 5. Dock Input Protection and Bus Architecture

- [x] Make dock-side module input protection mandatory. See [D-0005](decisions/0005-dock-input-protection.md).
- [x] Select exact dock input protection size and type for each module input: Blue Sea 285-Series 60A DC breaker per module input.
- [x] Confirm dock input breakers protect against reverse-feed faults from the common bus.
- [~] Define positive busbar rating, material, cover, and stud layout: covered 250A-class busbar selected; exact part/stud count pending layout.
- [~] Define negative busbar rating, material, cover, and stud layout: covered 250A-class busbar selected; exact part/stud count pending layout.
- [x] Define SmartShunt placement and wiring: Victron SmartShunt 500A on negative side.
- [x] Confirm all load and charge negatives land on the system side of the shunt.
- [x] Confirm only module/battery negatives land on the battery side of the shunt.
- [x] Define main dock output fuse type and holder: Littelfuse JLLN100 100A Class T fuse; holder family pending physical layout.
- [x] Confirm 100A dock output fuse DC voltage rating and interrupt rating: 160VDC, 20kA DC interrupt rating.
- [x] Define main output cable length and gauge: 2 AWG fine-strand copper; length pending physical layout.
- [x] Define future inverter takeoff location without bypassing shunt or protection: reserve physical space only; no energized inverter branch in v1.

Acceptance criteria:

- Every dock conductor connected to the common bus is protected from every source that can energize it.
- Busbar layout avoids excessive lug stacking and remains finger-safe during normal service.

## 6. Module Paralleling and Precharge / Equalization

- [x] Define required voltage-match threshold before paralleling: target 0.10V or less; absolute maximum 0.20V.
- [x] Add v1 precharge/equalization circuit. See [D-0007](decisions/0007-module-paralleling-precharge.md).
- [x] Select precharge resistor value and wattage: 25 ohm, 50W chassis resistor per module input.
- [x] Define precharge switch or keyed service connector: momentary precharge switch per module input.
- [x] Define visual or metered indication that modules are within safe delta: module positive, bus positive, and common negative test points.
- [x] Define operator sequence for adding second module: breaker off, connect SB120, compare voltage, hold precharge, confirm delta, close breaker, release precharge.
- [x] Define operator sequence for removing one module under load: turn off loads/chargers, open dock input breaker, open module disconnect, unplug SB120.
- [x] Define what loads and chargers must be off during connection/disconnection: all loads and charging sources off before adding/removing modules.
- [x] Decide whether SB120 connections are user-serviceable hot connections or only de-energized service connections: SB120 connections are de-energized service connections only.

Acceptance criteria:

- Two modules cannot be casually connected at large voltage delta.
- There is a written, repeatable procedure that avoids connector arcing and uncontrolled equalization current.

## 7. Wire, Lug, Crimp, and Harness Specification

- [~] Create final wire schedule with circuit name, current, fuse, wire gauge, insulation type, color, length, and termination: required after physical layout.
- [ ] Confirm 6 AWG module leads are compatible with chosen SB120 contacts.
- [ ] Confirm 2 AWG dock output leads are compatible with chosen SB120 contacts.
- [x] Choose cable type: marine-grade tinned fine-strand copper, 105C insulation where practical. See [D-0008](decisions/0008-wire-harness-and-cable-fabrication.md).
- [ ] Define high-current cable color convention.
- [ ] Define low-current accessory wire color convention.
- [~] Select exact crimp lugs and terminals: pending final wire schedule and stud/contact sizes.
- [x] Select crimp tool or service provider: v1 cables built in-house with proper crimp tooling.
- [x] Define adhesive heat-shrink requirements: adhesive-lined heat shrink required on every lug termination.
- [ ] Define abrasion sleeve and grommet requirements.
- [x] Define strain relief within 2-4 inches of each high-current connector.
- [~] Define max voltage-drop target per circuit: use conservative gauge selections; numeric targets to finalize in wire schedule.
- [~] Define max acceptable temperature rise under sustained load: final pass/fail limit to define in thermal validation section.
- [x] Add cable fabrication acceptance process: [Cable fabrication acceptance guide](guides/cable-fabrication-acceptance.md).

Acceptance criteria:

- Every conductor is sized to its fuse, load, run length, and environment.
- Every high-current termination has a specified terminal, crimp method, and strain relief.

## 8. Connector Strategy

- [x] Select exact Anderson SB120 housings and contacts for module inputs: gray SB120 housing 6810G1 with 1319G6 6 AWG contacts.
- [x] Select exact Anderson SB120 housing and contacts for main output: red SB120 housing 6810G3 with 1319 2 AWG contacts.
- [x] Define connector color/keying plan. See [D-0009](decisions/0009-connector-keying-strategy.md).
- [x] Confirm module connectors cannot mate with main output or inverter output if that would be unsafe: gray SB120 module inputs, red SB120 main output, blue SB175 future inverter.
- [x] Select environmental boots or covers for exposed SB connectors: SB120 source boot 3-6034P1 and load boot 3-6035P1, used where appropriate.
- [~] Select low-current accessory connectors: red/black Anderson Powerpole PP30/PP45 family, exact panel parts pending load layout.
- [x] Select solar connector/bulkhead type: Anderson Powerpole PP45 solar input with MC4-to-Powerpole adapter.
- [~] Select signal/service connector type if needed: Deutsch DTM 4-pin family selected for BMS display/service if final JK harness pinout matches.
- [x] Define connector labeling format: label every connector with function, nominal voltage, current limit/fuse, and source/load direction where relevant.

Acceptance criteria:

- Physically incompatible connectors prevent accidental cross-connection between battery, solar, 12V, 24V, and inverter circuits.
- All connectors have strain relief and abrasion protection.

## 9. Mechanical Enclosure and Sled Retention

- [!] Define module enclosure material and wall/plate thickness.
- [!] Define mechanical retention strategy independent of SB120 connector.
- [ ] Define sled rail/tray geometry.
- [ ] Define latch or clamp mechanism.
- [ ] Define handle placement and lifting method.
- [ ] Define module mass estimate.
- [ ] Define dock mass estimate.
- [ ] Define braking and shock load assumptions.
- [ ] Define how modules are prevented from moving forward, upward, and sideways.
- [ ] Define vibration isolation material.
- [ ] Confirm vibration isolation does not allow cable fatigue or connector fretting.
- [ ] Define service panel access.
- [ ] Define drain/ingress strategy for frunk environment.
- [ ] Define enclosure ventilation strategy.

Acceptance criteria:

- The battery sled is mechanically retained for vehicle motion and foreseeable hard braking.
- Electrical connectors are alignment aids and current paths, not structural restraints.

## 10. Cell Compression and Internal Pack Mechanics

- [ ] Confirm EVE LF105 compression recommendation from supplier/datasheet.
- [ ] Define end plate material and size.
- [ ] Define threaded rod/strap placement.
- [ ] Define insulation between cells, end plates, compression hardware, and enclosure.
- [ ] Define restraint against vertical and lateral movement.
- [ ] Confirm busbars are not used as structural members.
- [ ] Define cell terminal torque values.
- [ ] Define torque-marking process.
- [ ] Define cell access and inspection plan.

Acceptance criteria:

- Cells are compressed and restrained without risking wrapper damage or terminal stress.
- Electrical interconnects remain electrically and mechanically serviceable.

## 11. Thermal Design and Validation

- [ ] Define expected worst-case frunk ambient temperature.
- [ ] Define allowed sustained BMS temperature.
- [ ] Define allowed sustained connector/lug temperature rise.
- [ ] Define passive cooling paths.
- [ ] Decide whether BMS needs direct enclosure heat sinking.
- [ ] Decide whether DC-DC charger and MPPT need aluminum mounting plate heat spreading.
- [ ] Define thermal test equipment: IR camera, thermocouples, or both.
- [ ] Define single-module 25A test.
- [ ] Define single-module 50A test.
- [ ] Define dual-module 100A dock test.
- [ ] Define charging thermal test.
- [ ] Define closed-enclosure soak test.
- [ ] Define pass/fail limits.

Acceptance criteria:

- Thermal validation is performed with the enclosure in its real installed configuration.
- Any hot connection is corrected before field use.

## 12. Load Distribution and Accessory Outputs

- [ ] Confirm ICECO APL35 voltage range and connector strategy.
- [ ] Confirm Starlink Mini power input requirements and regulated supply choice.
- [ ] Select USB-C PD module(s) and confirm 24V compatibility.
- [ ] Define lighting load.
- [ ] Define small electronics load budget.
- [ ] Select 24V to 12V converter model and rating.
- [ ] Decide isolated vs non-isolated converter.
- [ ] Define 12V fuse block or branch protection.
- [ ] Define accessory output labeling.
- [ ] Confirm accessory outputs cannot be confused with battery/module connectors.

Acceptance criteria:

- Every load has a defined voltage source, fuse, connector, and expected current.
- The branch system cannot overload the 24V to 12V converter or its wiring.

## 13. Monitoring, Diagnostics, and Service Procedures

- [ ] Define SmartShunt model and current rating.
- [ ] Define SmartShunt configuration values: capacity, charged voltage, tail current, Peukert/exponent if used.
- [ ] Define BMS app/service access procedure.
- [ ] Define voltage test points for each module input and common bus.
- [ ] Define pre-departure checklist.
- [ ] Define module install checklist.
- [ ] Define module removal checklist.
- [ ] Define charging checklist.
- [ ] Define fault isolation procedure.
- [ ] Define spare fuse list.
- [ ] Define label map for all circuits.

Acceptance criteria:

- A field user can determine module voltage, fuse status, charge state, and load state without disassembling the system.

## 14. Future Inverter Integration

- [ ] Define whether inverter support is physically present in v1 or reserved only.
- [ ] Define maximum inverter DC input current allowed by v1 design.
- [ ] Select connector size: SB120 vs SB175.
- [ ] Define inverter fuse type and size.
- [ ] Confirm inverter negative path remains measured by SmartShunt.
- [ ] Define inverter cable gauge and max length.
- [ ] Define whether inverter use requires both modules installed.
- [ ] Define service warning label for inverter branch.

Acceptance criteria:

- Future inverter integration cannot bypass dock protection, shunt measurement, or connector keying.
- Any inverter above the 100A dock design target triggers a separate design review.

## 15. Commissioning and Acceptance Tests

- [ ] Cell voltage verification before BMS connection.
- [ ] BMS sense lead order verification.
- [ ] Insulation/continuity check before first energization.
- [ ] Polarity check at every connector.
- [ ] Fuse value verification.
- [ ] Torque mark verification.
- [ ] No-load power-up test.
- [ ] Single-module low-current load test.
- [ ] Single-module 50A load test.
- [ ] Dual-module voltage-match test.
- [ ] Dual-module 100A combined load test.
- [ ] Charger function test.
- [ ] Solar function test.
- [ ] Accessory branch load test.
- [ ] Thermal inspection after sustained load.
- [ ] Road vibration inspection after first drive.
- [ ] Post-test retorque inspection if required by component manufacturer.

Acceptance criteria:

- The system passes electrical, thermal, mechanical, and service checks before being treated as field-ready.

## 16. Open Decisions Log

Use this section to capture decisions as they are made.

| Date | Area | Decision | Evidence / Link | Follow-up |
|---|---|---|---|---|
| 2026-05-23 | Baseline | Keep modular 8S battery sled + shared dock architecture. | Existing design brief and review. | Resolve build-readiness blockers. |

## 17. Blocking Items Summary

These must be resolved before physical build starts:

- [!] Exact DC-DC charger model and 24V charge compatibility.
- [!] Exact JK BMS model and settings.
- [!] Module fuse type, DC rating, and interrupt rating.
- [!] Mandatory dock-side module input protection or equivalent reverse-feed protection.
- [!] Required precharge/equalization procedure or circuit.
- [!] Mechanical sled retention strategy independent of connectors.
- [!] Exact MPPT and PV string design.
