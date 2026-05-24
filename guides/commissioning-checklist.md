# Commissioning Checklist

Do not treat the system as field-ready until these checks pass.

## Pre-Energization

- Verify every cell voltage before BMS harness connection.
- Verify BMS sense lead order.
- Verify pack polarity at module SB120 before connecting to dock.
- Verify fuse values and breaker values.
- Verify torque marks on cell terminals, busbars, fuses, breakers, shunt, and switches.
- Verify no cable strain at SB120 connectors, fuse holders, breakers, or busbars.
- Verify all exposed live parts are covered.

## First Power-Up

- Start with one module.
- Dock input breaker open.
- Module disconnect open.
- Connect SB120.
- Close module disconnect.
- Use precharge path and verify bus/module voltage delta.
- Close dock input breaker.
- Confirm SmartShunt/BMS current is sane near zero load.

## Load Tests

- Single-module 10A load for 15 minutes.
- Single-module 25A load for 30 minutes.
- Single-module 50A load for 30 minutes.
- Dual-module voltage-match check.
- Dual-module 100A dock output test for 30 minutes if a suitable load is available.

## Charging Tests

- AC charger test at 25A output.
- Solar MPPT test with PV disconnect procedure.
- Do not intentionally run AC and solar charging together in v1.
- Confirm BMS charge current and charger state agree.

## Thermal Pass/Fail

- Use IR camera and contact thermocouples.
- Check SB120 contacts, fuse holders, breakers, shunt, busbars, lugs, BMS, AC charger, MPPT, and DC converter.
- Pass if no connector/lug/fuse/breaker is more than 20C above comparable nearby cable under sustained load.
- Pass if all devices remain below manufacturer temperature ratings.
- Remake or repair any hot termination before field use.

## Road/Vibration Follow-Up

- Inspect after first short drive.
- Inspect after first off-road or rough-road use.
- Look for cable movement, connector fretting, latch movement, loose fasteners, and shifted insulation.
- Retorque only where the component manufacturer allows retorque.

