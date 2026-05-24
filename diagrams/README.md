# Diagrams

This folder contains source diagrams for the auxiliary power-system design.

Keep diagrams as editable text where possible. Mermaid files are preferred for architecture, wiring, and flow diagrams because they can be reviewed in diffs and linked from design notes.

## Planned Diagrams

- [x] [`charging-input-architecture.mmd`](charging-input-architecture.mmd) - AC shore, Rivian 120V, and solar charging paths.
- [x] [`dc-dc-charger-architecture.mmd`](dc-dc-charger-architecture.mmd) - deferred optional DC-DC charger source, control, and dock integration.
- [x] [`precharge-equalization.mmd`](precharge-equalization.mmd) - per-input module precharge/equalization circuit.
- [ ] `system-architecture.mmd` - full system block diagram.
- [ ] `battery-module-wiring.mmd` - per-module electrical schematic.
- [ ] `dock-controller-wiring.mmd` - dock/controller wiring architecture.
- [ ] `busbar-topology.mmd` - positive/negative busbar and shunt topology.
- [ ] `module-physical-layout.mmd` - battery sled physical layout.
- [ ] `dock-physical-layout.mmd` - dock physical layout.
- [ ] `service-sequence.mmd` - safe install/remove/charge service sequence.

## Conventions

- Use one diagram per file.
- Prefer stable node names so diffs stay readable.
- Include voltage/current labels where they affect design decisions.
- Link diagrams from the checklist once they become canonical.
