# Diagrams

This folder contains source diagrams for the auxiliary power-system design.

Keep diagrams as editable text where possible. Mermaid files are preferred for architecture, wiring, and flow diagrams because they can be reviewed in diffs and linked from design notes.

## Planned Diagrams

- [ ] `system-architecture.mmd` - full system block diagram.
- [ ] `battery-module-wiring.mmd` - per-module electrical schematic.
- [ ] `dock-controller-wiring.mmd` - dock/controller wiring architecture.
- [ ] `busbar-topology.mmd` - positive/negative busbar and shunt topology.
- [ ] `module-physical-layout.mmd` - battery sled physical layout.
- [ ] `dock-physical-layout.mmd` - dock physical layout.
- [ ] `precharge-equalization.mmd` - module paralleling and precharge/equalization flow.
- [ ] `service-sequence.mmd` - safe install/remove/charge service sequence.

## Conventions

- Use one diagram per file.
- Prefer stable node names so diffs stay readable.
- Include voltage/current labels where they affect design decisions.
- Link diagrams from the checklist once they become canonical.

