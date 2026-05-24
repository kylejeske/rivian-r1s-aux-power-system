# Service Procedures

## Pre-Departure

- Confirm modules are latched and mechanically retained.
- Confirm module voltages are within 0.10V if both modules will be paralleled.
- Confirm dock breakers match intended module use.
- Confirm AC charger is unplugged if using solar.
- Confirm solar is disconnected if using AC charging.
- Confirm branch fuse spares are present.

## Add A Module

1. Turn off loads and charging sources.
2. Open the target dock input breaker.
3. Confirm the module disconnect is open.
4. Insert module into rails and latch it.
5. Connect gray SB120.
6. Measure module positive to common negative.
7. Measure bus positive to common negative.
8. If delta is above 0.20V, stop and balance module SOC separately.
9. Hold precharge switch.
10. Confirm delta is 0.10V or less.
11. Close dock input breaker.
12. Release precharge.
13. Confirm BMS/SmartShunt current is normal.

## Remove A Module

1. Turn off loads and charging sources.
2. Open that module's dock input breaker.
3. Confirm module current is near 0A.
4. Open module service disconnect.
5. Unplug gray SB120.
6. Release mechanical latch.
7. Remove module.

## AC Charging

1. Confirm solar is disconnected.
2. Connect one 120VAC source only.
3. Confirm AC inlet strain relief and cord condition.
4. Start Phoenix Smart IP43 charger.
5. Confirm charge current is about 25A or less.
6. Monitor first 15 minutes for heat, smell, noise, or BMS alarms.

## Solar Charging

1. Confirm AC charger is unplugged/off.
2. Confirm PV disconnect is open.
3. Connect solar panel adapter.
4. Close PV disconnect.
5. Confirm MPPT sees PV voltage and battery voltage.
6. Monitor first 15 minutes for heat or connector issues.

## Fault Isolation

- If a module input trips: turn off loads/chargers, leave breaker open, inspect module voltage and cable path.
- If module BMS trips: do not bypass it; inspect BMS fault reason.
- If main output fuse opens: inspect downstream loads and main output wiring before replacing fuse.
- If any connector is hot: stop using that circuit until the termination is inspected or remade.

