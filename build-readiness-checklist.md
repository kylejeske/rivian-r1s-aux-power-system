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
- [x] Create project documentation folders for diagrams, schemas, structured data, and decisions.
- [x] Record final system block diagram revision in [`diagrams/system-architecture.mmd`](diagrams/system-architecture.mmd).
- [x] Record final per-module wiring schematic revision in [`diagrams/battery-module-wiring.mmd`](diagrams/battery-module-wiring.mmd).
- [x] Record final dock/controller schematic revision in [`diagrams/dock-controller-wiring.mmd`](diagrams/dock-controller-wiring.mmd).
- [x] Record final physical layout drawing revision in [`diagrams/`](diagrams/): module and dock physical layout diagrams added.
- [x] Define reusable information schemas in [`schemas/`](schemas/).
- [x] Store reusable design data in [`data/`](data/).
- [x] Record accepted design decisions in [`decisions/`](decisions/).

Acceptance criteria:

- One canonical schematic set exists and matches the BOM, wiring table, fuse table, and assembly sequence.
- Checklist items that close safety-critical decisions link to their diagram, schema/data entry, or decision record.

## 1. Charger Selection and Charge Architecture

- [x] Identify intended charging paths: 120V shore power, Rivian 120V outlet, and solar input. See [D-0002](decisions/0002-charging-input-paths.md).
- [x] Defer DC-DC charging unless a future 12V/24V DC source is intentionally added. See [D-0001](decisions/0001-dc-dc-charger-architecture.md).
- [x] Define AC charger output class: 24V 25A target, roughly 600W DC output.
- [x] Select exact AC-to-24V LiFePO4 charger model: Victron Phoenix Smart IP43 24/25.
- [x] Define AC input method: covered 15A 120VAC inlet, 14 AWG internal AC wiring, hot-side 10A protection, equipment ground to metal enclosure if used, upstream GFCI assumed.
- [x] Confirm AC charger draw stays within Rivian 120V outlet limit and shore-power assumptions. 24V 25A target is comfortably below Rivian 1500W inverter limit.
- [x] Define AC charger DC output current for one-module and two-module operation: same 25A charger target for either one or two modules.
- [x] Add AC charger-specific fuse sizes to fuse table: 10A AC hot-side protection; 40A DC output protection pending manual confirmation.
- [x] Add AC charger-specific wire sizes to wire table: 14 AWG AC input wiring; 8 AWG DC output wiring.
- [x] Add AC charger mounting requirements to dock physical layout: vertical serviceable mounting, airflow around charger, AC strain relief, AC/DC separation.
- [x] Define absorption voltage, float voltage, re-bulk behavior, and charge termination behavior: absorption 28.2V, float 27.2V, no equalization, charger current limit 25A.
- [x] Define low-temperature charge cutoff strategy: BMS charge cutoff at 2C with 5C recovery; do not charge cold modules.
- [x] Define behavior when BMS disconnects during charging: stop charger/MPPT, investigate BMS fault, do not bypass BMS.
- [x] Confirm whether charger requires direct battery sense or can tolerate dock-side switching: charger lands on dock bus; modules must be connected before charging.

Acceptance criteria:

- Exact AC charger SKU is chosen.
- Its datasheet/manual explicitly supports the planned input and output voltages.
- Charge settings are written down before hardware is purchased.
- Failure behavior is understood for BMS disconnect, charger fault, source undervoltage, and module removal.

## 2. Solar / MPPT Architecture

- [x] Select exact Victron SmartSolar MPPT model: SmartSolar MPPT 100/30.
- [x] Define solar panel count, panel Voc, Vmp, Isc, and Imp. Target: portable 2S array, 200W-500W nominal, 36V-44V Vmp, cold-corrected Voc below 75V, Isc no higher than 15A at dock input.
- [x] Calculate cold-weather corrected Voc: final panel check required before purchase; v1 spec caps cold-corrected Voc at 75V for margin below 100V controller limit.
- [x] Confirm PV string voltage never exceeds MPPT input limit. Target leaves margin below 100V controller limit.
- [x] Confirm PV operating voltage is high enough for a 24V battery bank: 2S portable-panel target keeps Vmp above battery voltage.
- [x] Decide whether panels are series, parallel, or series-parallel: prefer 2S portable-panel configuration.
- [x] Define PV disconnect location: dock-side solar input disconnect/breaker between solar connector and MPPT.
- [x] Define PV fuse/breaker needs, especially if using parallel strings: 15A PV disconnect/breaker for v1 single 2S string; re-evaluate for parallel strings.
- [x] Define MPPT battery-side fuse size from Victron manual: 40A DC protection on MPPT battery positive.
- [x] Define MPPT battery-side wire gauge and run length: 8 AWG, kept short inside dock.
- [x] Define temperature sense strategy for MPPT charging: BMS enforces cell temperature; disable solar if BMS temperature fault occurs.
- [x] Define what happens when modules are removed while solar is connected: open PV disconnect and turn off charging before module removal.

Acceptance criteria:

- PV design is valid at lowest expected ambient temperature.
- MPPT battery-side fuse and wire sizes match the selected controller manual.
- There is a safe service sequence for solar disconnect before battery/module removal.

## 3. Module BMS Selection and Configuration

- [x] Select exact JK BMS model and current rating: JK-B2A8S20P, 200A class. See [D-0003](decisions/0003-bms-selection-and-charge-policy.md).
- [x] Confirm BMS supports 8S LiFePO4.
- [x] Confirm continuous discharge current rating exceeds 60A fuse and 50A operating target with margin.
- [x] Confirm charge current rating exceeds planned charger current. V1 operating policy is one charging source at a time, so normal charge current is 25A AC or up to 30A solar.
- [x] Confirm BMS thermal behavior inside the planned enclosure: specified as commissioning thermal gate; BMS MOS temp must remain below 70C in sustained 50A module test.
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
- [x] Confirm fuse can be mounted close enough to pack positive: fuse must mount inside module service bay adjacent to pack positive.
- [x] Select exact manual disconnect: Blue Sea 6006 m-Series battery switch.
- [x] Confirm disconnect is DC-rated for pack voltage and current: 48VDC max, 300A continuous.
- [x] Confirm disconnect can break expected load current without damage: treat as no-load service isolator only; do not use for normal load breaking.
- [x] Define module service sequence: turn off loads and chargers, verify near-zero current, open disconnect, then unplug SB120.
- [x] Define module fuse replacement access: service panel must expose fuse holder without unpacking cell stack.
- [x] Add insulated covers for fuse, disconnect, and pack positive path: required over all live studs and bus paths.

Acceptance criteria:

- The first conductor leaving pack positive is protected as close to the cell stack as practical.
- Fuse and disconnect ratings are documented by datasheet, not inferred from current alone.

## 5. Dock Input Protection and Bus Architecture

- [x] Make dock-side module input protection mandatory. See [D-0005](decisions/0005-dock-input-protection.md).
- [x] Select exact dock input protection size and type for each module input: Blue Sea 285-Series 60A DC breaker per module input.
- [x] Confirm dock input breakers protect against reverse-feed faults from the common bus.
- [x] Define positive busbar rating, material, cover, and stud layout: covered 250A-class copper busbar, 6+ studs preferred, avoid more than two lugs per stud.
- [x] Define negative busbar rating, material, cover, and stud layout: covered 250A-class copper busbar, 6+ studs preferred, avoid more than two lugs per stud.
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

- [x] Create final wire schedule with circuit name, current, fuse, wire gauge, insulation type, color, length, and termination: baseline gauges defined; final measured lengths recorded during fabrication.
- [x] Confirm 6 AWG module leads are compatible with chosen SB120 contacts: 1319G6 contact.
- [x] Confirm 2 AWG dock output leads are compatible with chosen SB120 contacts: 1319 contact.
- [x] Choose cable type: marine-grade tinned fine-strand copper, 105C insulation where practical. See [D-0008](decisions/0008-wire-harness-and-cable-fabrication.md).
- [x] Define high-current cable color convention: red positive, black negative, yellow/black solar input, white/green/black AC per cord convention.
- [x] Define low-current accessory wire color convention: red regulated positive, black return, yellow signal/service, blue switched/control.
- [x] Select exact crimp lugs and terminals: tinned copper closed-barrel lugs sized to conductor/stud; Anderson contacts as specified in connector strategy.
- [x] Select crimp tool or service provider: v1 cables built in-house with proper crimp tooling.
- [x] Define adhesive heat-shrink requirements: adhesive-lined heat shrink required on every lug termination.
- [x] Define abrasion sleeve and grommet requirements: abrasion sleeve on all mobile runs; grommets/cable glands at every enclosure pass-through.
- [x] Define strain relief within 2-4 inches of each high-current connector.
- [x] Define max voltage-drop target per circuit: high-current paths target 3% or less; accessory/USB paths target 5% or less.
- [x] Define max acceptable temperature rise under sustained load: no termination more than 20C above comparable nearby cable.
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
- [x] Select low-current accessory connectors: red/black Anderson Powerpole PP30/PP45 family for regulated accessory outputs.
- [x] Select solar connector/bulkhead type: Anderson Powerpole PP45 solar input with MC4-to-Powerpole adapter.
- [x] Select signal/service connector type if needed: Deutsch DTM 4-pin family for BMS display/service; adjust pin count only if JK harness requires it.
- [x] Define connector labeling format: label every connector with function, nominal voltage, current limit/fuse, and source/load direction where relevant.

Acceptance criteria:

- Physically incompatible connectors prevent accidental cross-connection between battery, solar, 12V, 24V, and inverter circuits.
- All connectors have strain relief and abrasion protection.

## 9. Mechanical Enclosure and Sled Retention

- [x] Define module enclosure material and wall/plate thickness: aluminum enclosure, 0.100 in minimum panels, 0.125 in base/end structural plates, nonconductive internal liners. See [D-0010](decisions/0010-mechanical-enclosure-and-retention.md).
- [x] Define mechanical retention strategy independent of SB120 connector: guided tray, positive latches, secondary retention; connectors are not structural.
- [x] Define sled rail/tray geometry: two guided rails per module with hard stops forward/aft and lateral capture.
- [x] Define latch or clamp mechanism: two positive latches or clamps per module with secondary safety pin/retainer.
- [x] Define handle placement and lifting method: two recessed handles per module, clear of live service area.
- [x] Define module mass estimate: design retention around 75 lb per loaded module until measured.
- [x] Define dock mass estimate: design retention around 35 lb dock mass until measured.
- [x] Define braking and shock load assumptions: 5g forward, 3g lateral, 3g vertical.
- [x] Define how modules are prevented from moving forward, upward, and sideways: rails, hard stops, latches, and secondary retention.
- [x] Define vibration isolation material: neoprene/EPDM pads under constrained rails/tray.
- [x] Confirm vibration isolation does not allow cable fatigue or connector fretting: isolation must not permit connector-borne load or cable tension.
- [x] Define service panel access: fuse, disconnect, BMS service port, and BMS visibility accessible without cell-stack disassembly.
- [x] Define drain/ingress strategy for frunk environment: electronics elevated from floor, cable glands/grommets, drain path below electronics.
- [x] Define enclosure ventilation strategy: passive/labyrinth venting and air gap around BMS/electronics.

Acceptance criteria:

- The battery sled is mechanically retained for vehicle motion and foreseeable hard braking.
- Electrical connectors are alignment aids and current paths, not structural restraints.

## 10. Cell Compression and Internal Pack Mechanics

- [x] Confirm EVE LF105 compression recommendation from supplier/datasheet: use dedicated compression/restraint frame; verify exact supplier force/torque documentation before final assembly. See [D-0011](decisions/0011-cell-compression-and-pack-mechanics.md).
- [x] Define end plate material and size: 0.125 in aluminum end plates with G10/fiberglass insulation against cells.
- [x] Define threaded rod/strap placement: four 1/4-20 insulated rods outside cell bodies or equivalent external straps.
- [x] Define insulation between cells, end plates, compression hardware, and enclosure: G10/fiberglass or fishpaper barriers at all contact points.
- [x] Define restraint against vertical and lateral movement: nonconductive cell spacers/liners plus compression frame tied to module base.
- [x] Confirm busbars are not used as structural members.
- [x] Define cell terminal torque values: use purchased-cell supplier value; do not exceed cell-terminal documentation.
- [x] Define torque-marking process: torque stripe every terminal, busbar, fuse, breaker, switch, and shunt fastener.
- [x] Define cell access and inspection plan: removable service cover for visual inspection and terminal torque-mark verification.

Acceptance criteria:

- Cells are compressed and restrained without risking wrapper damage or terminal stress.
- Electrical interconnects remain electrically and mechanically serviceable.

## 11. Thermal Design and Validation

- [x] Define expected worst-case frunk ambient temperature: 50C design ambient for validation. See [D-0013](decisions/0013-thermal-validation.md).
- [x] Define allowed sustained BMS temperature: BMS MOS temperature below 70C during sustained 50A module test unless JK manual is stricter.
- [x] Define allowed sustained connector/lug temperature rise: no termination more than 20C above comparable nearby cable.
- [x] Define passive cooling paths: aluminum enclosure/heat spreaders, air gaps, passive/labyrinth vents.
- [x] Decide whether BMS needs direct enclosure heat sinking: mount with thermal path/air gap; add heat spreader if commissioning shows hot spots.
- [x] Decide whether DC-DC charger and MPPT need aluminum mounting plate heat spreading: AC charger, MPPT, and 24/12 converter mount to aluminum heat-spreader plate.
- [x] Define thermal test equipment: IR camera plus contact thermocouples.
- [x] Define single-module 25A test: 30 minutes closed enclosure.
- [x] Define single-module 50A test: 30 minutes closed enclosure.
- [x] Define dual-module 100A dock test: 30 minutes if suitable load is available.
- [x] Define charging thermal test: AC charger at 25A and solar MPPT test separately.
- [x] Define closed-enclosure soak test: run load/charge tests with final covers installed.
- [x] Define pass/fail limits: component ratings not exceeded, no hot termination, no softened insulation, no smell/noise/deformation.

Acceptance criteria:

- Thermal validation is performed with the enclosure in its real installed configuration.
- Any hot connection is corrected before field use.

## 12. Load Distribution and Accessory Outputs

- [x] Confirm ICECO APL35 voltage range and connector strategy: fused 24V branch, 12 AWG, 15A fuse, Powerpole/accessory output. See [D-0012](decisions/0012-load-distribution-and-accessories.md).
- [x] Confirm Starlink Mini power input requirements and regulated supply choice: fused native 24V branch where practical, 12 AWG, 10A fuse.
- [x] Select USB-C PD module(s) and confirm 24V compatibility: 24V-compatible 100W USB-C PD panel modules, exact part pending purchase.
- [x] Define lighting load: 24V or regulated 12V branch, 5A fuse unless actual lighting requires less.
- [x] Define small electronics load budget: reserve 10A at 12V regulated output for miscellaneous small electronics.
- [x] Select 24V to 12V converter model and rating: Victron Orion-Tr 24/12-20 isolated.
- [x] Decide isolated vs non-isolated converter: isolated converter selected.
- [x] Define 12V fuse block or branch protection: converter input 15A, output max 25A, downstream fused accessory circuits.
- [x] Define accessory output labeling: label voltage, fuse/current limit, and regulated/unregulated status.
- [x] Confirm accessory outputs cannot be confused with battery/module connectors: Powerpole accessory outputs only, no SB connectors.

Acceptance criteria:

- Every load has a defined voltage source, fuse, connector, and expected current.
- The branch system cannot overload the 24V to 12V converter or its wiring.

## 13. Monitoring, Diagnostics, and Service Procedures

- [x] Define SmartShunt model and current rating: Victron SmartShunt 500A. See [D-0014](decisions/0014-monitoring-service-and-inverter-boundary.md).
- [x] Define SmartShunt configuration values: 105Ah one module, 210Ah two modules, charged voltage 28.0V, tail current 4%, Peukert 1.05.
- [x] Define BMS app/service access procedure: Bluetooth plus wired JK display/service connector.
- [x] Define voltage test points for each module input and common bus: module positive, bus positive, common negative at each input/precharge position.
- [x] Define pre-departure checklist: added to [service procedures](guides/service-procedures.md).
- [x] Define module install checklist: added to [service procedures](guides/service-procedures.md).
- [x] Define module removal checklist: added to [service procedures](guides/service-procedures.md).
- [x] Define charging checklist: AC and solar procedures added to [service procedures](guides/service-procedures.md).
- [x] Define fault isolation procedure: added to [service procedures](guides/service-procedures.md).
- [x] Define spare fuse list: JLLN060, JLLN100, 2A precharge fuses, branch fuses, AC input fuse/breaker spare where applicable.
- [x] Define label map for all circuits: function, voltage, current/fuse limit, source/load direction, and service warning labels required.

Acceptance criteria:

- A field user can determine module voltage, fuse status, charge state, and load state without disassembling the system.

## 14. Future Inverter Integration

- [x] Define whether inverter support is physically present in v1 or reserved only: reserved physical space only; no energized branch in v1.
- [x] Define maximum inverter DC input current allowed by v1 design: v1 dock output remains 100A max; inverter above 100A requires separate design review.
- [x] Select connector size: SB175 blue reserved for future inverter path, not installed in v1.
- [x] Define inverter fuse type and size: not installed in v1; future inverter requires dedicated Class T fuse sized to inverter.
- [x] Confirm inverter negative path remains measured by SmartShunt: required for any future inverter branch.
- [x] Define inverter cable gauge and max length: future branch requires separate design; likely 2 AWG minimum for <=100A short run.
- [x] Define whether inverter use requires both modules installed: future inverter use above 50A should require both modules installed.
- [x] Define service warning label for inverter branch: "INVERTER RESERVED - NOT ENERGIZED IN V1".

Acceptance criteria:

- Future inverter integration cannot bypass dock protection, shunt measurement, or connector keying.
- Any inverter above the 100A dock design target triggers a separate design review.

## 15. Commissioning and Acceptance Tests

- [x] Cell voltage verification before BMS connection: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] BMS sense lead order verification: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Insulation/continuity check before first energization: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Polarity check at every connector: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Fuse value verification: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Torque mark verification: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] No-load power-up test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Single-module low-current load test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Single-module 50A load test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Dual-module voltage-match test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Dual-module 100A combined load test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Charger function test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Solar function test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Accessory branch load test: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Thermal inspection after sustained load: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Road vibration inspection after first drive: defined in [commissioning checklist](guides/commissioning-checklist.md).
- [x] Post-test retorque inspection if required by component manufacturer: defined in [commissioning checklist](guides/commissioning-checklist.md).

Acceptance criteria:

- The system passes electrical, thermal, mechanical, and service checks before being treated as field-ready.

## 16. Open Decisions Log

Use this section to capture decisions as they are made.

| Date | Area | Decision | Evidence / Link | Follow-up |
|---|---|---|---|---|
| 2026-05-23 | Baseline | Keep modular 8S battery sled + shared dock architecture. | Existing design brief and review. | Resolve build-readiness blockers. |

## 17. Blocking Items Summary

These must be resolved before physical build starts:

- [x] DC-DC charger removed from v1; v1 uses 120VAC charger plus solar MPPT.
- [x] Exact JK BMS model and baseline settings selected.
- [x] Module fuse type, DC rating, and interrupt rating selected.
- [x] Mandatory dock-side module input protection selected.
- [x] Required precharge/equalization procedure and circuit selected.
- [x] Mechanical sled retention strategy independent of connectors defined.
- [x] Exact MPPT model and v1 PV design envelope defined.

Remaining build gates:

- [ ] Final frunk measurements and enclosure CAD.
- [ ] Final purchased solar panel datasheet check against PV voltage/current envelope.
- [ ] Final purchased-cell terminal torque and compression guidance check.
- [ ] Physical build, cable acceptance, commissioning, and thermal validation.
