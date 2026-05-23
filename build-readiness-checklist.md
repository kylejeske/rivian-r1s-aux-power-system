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

- [!] Identify exact DC-DC charger model.
- [!] Confirm charger supports the intended source voltage and 8S/24V LiFePO4 output.
- [ ] Identify source for DC-DC charging: Rivian 12V, external DC supply, shore charger, or other.
- [ ] Confirm whether the charger is isolated or non-isolated.
- [ ] Define charger enable/disable control strategy.
- [ ] Define input current limit so the Rivian/source system is not overloaded.
- [ ] Define output current limit for one-module and two-module operation.
- [ ] Define absorption voltage, float voltage, re-bulk behavior, and charge termination behavior.
- [ ] Define low-temperature charge cutoff strategy.
- [ ] Define behavior when BMS disconnects during charging.
- [ ] Confirm whether charger requires direct battery sense or can tolerate dock-side switching.
- [ ] Add charger-specific fuse sizes to fuse table.
- [ ] Add charger-specific wire sizes to wire table.

Acceptance criteria:

- Exact charger SKU is chosen.
- Its datasheet/manual explicitly supports the planned input and output voltages.
- Charge settings are written down before hardware is purchased.
- Failure behavior is understood for BMS disconnect, charger fault, source undervoltage, and module removal.

## 2. Solar / MPPT Architecture

- [!] Select exact Victron SmartSolar MPPT model.
- [ ] Define solar panel count, panel Voc, Vmp, Isc, and Imp.
- [ ] Calculate cold-weather corrected Voc.
- [ ] Confirm PV string voltage never exceeds MPPT input limit.
- [ ] Confirm PV operating voltage is high enough for a 24V battery bank.
- [ ] Decide whether panels are series, parallel, or series-parallel.
- [ ] Define PV disconnect location.
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

- [!] Select exact JK BMS model and current rating.
- [ ] Confirm BMS supports 8S LiFePO4.
- [ ] Confirm continuous discharge current rating exceeds 60A fuse and 50A operating target with margin.
- [ ] Confirm charge current rating exceeds planned charger current.
- [ ] Confirm BMS thermal behavior inside the planned enclosure.
- [ ] Define cell over-voltage cutoff and recovery.
- [ ] Define cell under-voltage cutoff and recovery.
- [ ] Define pack over-current cutoff and delay.
- [ ] Define charge low-temperature cutoff.
- [ ] Define discharge low-temperature cutoff.
- [ ] Define high-temperature charge/discharge cutoffs.
- [ ] Define active balancing start voltage and delta threshold.
- [ ] Confirm number and placement of temperature sensors.
- [ ] Decide whether BMS Bluetooth access is sufficient or if service access is needed.

Acceptance criteria:

- Exact BMS settings are recorded.
- BMS limits coordinate with charger settings instead of fighting them.
- BMS is not the only planned protection for normal charger control.

## 4. Module Fuse, Disconnect, and Fault Protection

- [!] Select exact 60A module fuse type and holder.
- [!] Confirm module fuse DC voltage rating and interrupt rating are adequate for 8S LiFePO4 fault current.
- [ ] Decide Class T vs MRBF vs other module fuse format.
- [ ] Confirm fuse can be mounted close enough to pack positive.
- [ ] Select exact manual disconnect.
- [ ] Confirm disconnect is DC-rated for pack voltage and current.
- [ ] Confirm disconnect can break expected load current without damage.
- [ ] Define module service sequence.
- [ ] Define module fuse replacement access.
- [ ] Add insulated covers for fuse, disconnect, and pack positive path.

Acceptance criteria:

- The first conductor leaving pack positive is protected as close to the cell stack as practical.
- Fuse and disconnect ratings are documented by datasheet, not inferred from current alone.

## 5. Dock Input Protection and Bus Architecture

- [!] Make dock-side module input fusing mandatory or document an equivalent protection method.
- [ ] Select exact dock input fuse size and type for each module input.
- [ ] Confirm dock input fuses protect against reverse-feed faults from the common bus.
- [ ] Define positive busbar rating, material, cover, and stud layout.
- [ ] Define negative busbar rating, material, cover, and stud layout.
- [ ] Define SmartShunt placement and wiring.
- [ ] Confirm all load and charge negatives land on the system side of the shunt.
- [ ] Confirm only module/battery negatives land on the battery side of the shunt.
- [ ] Define main dock output fuse type and holder.
- [ ] Confirm 100A dock output fuse DC voltage rating and interrupt rating.
- [ ] Define main output cable length and gauge.
- [ ] Define future inverter takeoff location without bypassing shunt or protection.

Acceptance criteria:

- Every dock conductor connected to the common bus is protected from every source that can energize it.
- Busbar layout avoids excessive lug stacking and remains finger-safe during normal service.

## 6. Module Paralleling and Precharge / Equalization

- [!] Define required voltage-match threshold before paralleling.
- [!] Add v1 precharge/equalization circuit or explicit no-hot-connect service rule.
- [ ] Select precharge resistor value and wattage.
- [ ] Define precharge switch or keyed service connector.
- [ ] Define visual or metered indication that modules are within safe delta.
- [ ] Define operator sequence for adding second module.
- [ ] Define operator sequence for removing one module under load.
- [ ] Define what loads and chargers must be off during connection/disconnection.
- [ ] Decide whether SB120 connections are user-serviceable hot connections or only de-energized service connections.

Acceptance criteria:

- Two modules cannot be casually connected at large voltage delta.
- There is a written, repeatable procedure that avoids connector arcing and uncontrolled equalization current.

## 7. Wire, Lug, Crimp, and Harness Specification

- [ ] Create final wire schedule with circuit name, current, fuse, wire gauge, insulation type, color, length, and termination.
- [ ] Confirm 6 AWG module leads are compatible with chosen SB120 contacts.
- [ ] Confirm 2 AWG or 4 AWG dock output leads are compatible with chosen SB120/SB175 contacts.
- [ ] Choose cable type: marine-grade tinned fine-strand preferred.
- [ ] Define high-current cable color convention.
- [ ] Define low-current accessory wire color convention.
- [ ] Select exact crimp lugs and terminals.
- [ ] Select crimp tool or service provider.
- [ ] Define adhesive heat-shrink requirements.
- [ ] Define abrasion sleeve and grommet requirements.
- [ ] Define strain relief within 2-4 inches of each high-current connector.
- [ ] Define max voltage-drop target per circuit.
- [ ] Define max acceptable temperature rise under sustained load.

Acceptance criteria:

- Every conductor is sized to its fuse, load, run length, and environment.
- Every high-current termination has a specified terminal, crimp method, and strain relief.

## 8. Connector Strategy

- [ ] Select exact Anderson SB120 housings and contacts for module inputs.
- [ ] Select exact Anderson SB120 or SB175 housing and contacts for main output.
- [ ] Define connector color/keying plan.
- [ ] Confirm module connectors cannot mate with main output or inverter output if that would be unsafe.
- [ ] Select environmental boots or covers for exposed SB connectors.
- [ ] Select low-current accessory connectors.
- [ ] Select solar connector/bulkhead type.
- [ ] Select signal/service connector type if needed.
- [ ] Define connector labeling format.

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
