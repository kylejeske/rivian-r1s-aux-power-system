# Rivian R1S Modular Auxiliary Power System

Design workspace for a modular auxiliary power system for a Rivian R1S.

The system concept uses removable 8S LiFePO4 battery sleds and a shared dock for charging, monitoring, paralleling, and DC load distribution. The current focus is making the design build-ready by resolving charger selection, dock protection, module paralleling, mechanical retention, thermal validation, and commissioning details.

Start here:

- [V1 build spec](v1-build-spec.md)
- [Build-readiness checklist](build-readiness-checklist.md)

Project references:

- [Diagrams](diagrams/)
- [Information schemas](schemas/)
- [Structured design data](data/)
- [Design decisions](decisions/)
- [Build and service guides](guides/)

Working rule:

- As design choices are made, update the checklist first.
- Add or update diagrams and structured data when a choice affects wiring, layout, component selection, validation, or service procedure.
- Link accepted decisions back to the checklist section they close.

V1 build-ready status:

- The electrical architecture, protection strategy, charging paths, BMS settings, connector keying, precharge behavior, mechanical baseline, load distribution, service procedures, and commissioning tests are specified.
- Remaining gates are physical measurement/CAD, purchased-part datasheet confirmation, cable fabrication acceptance, and commissioning/thermal validation.
