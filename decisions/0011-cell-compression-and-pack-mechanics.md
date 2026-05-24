# Decision: Cell Compression and Pack Mechanics

Status: accepted
Date: 2026-05-24

## Context

The module uses eight EVE LF105 prismatic LiFePO4 cells. The cells must be restrained, insulated, and compressed without making electrical interconnects structural.

## Decision

Use a dedicated compression frame inside each module: G10/fiberglass insulation between cells and metal structure, 0.125 in aluminum end plates, and four 1/4-20 insulated threaded rods or equivalent external straps.

Cell busbars are electrical only. They are not structural restraints.

## Open Questions

- Confirm exact LF105 terminal torque from the purchased cell supplier documentation.
- Confirm final compression gap/force after the actual cells and compression hardware are measured.

## Evidence

- Prismatic cells need restraint against swelling and vibration.
- A separate compression frame avoids transferring vehicle loads through terminals or busbars.

## Consequences

- Add insulating sheets between cells, end plates, rods/straps, and enclosure.
- Add vertical and lateral restraint so cells cannot walk under vibration.
- Torque-mark every cell terminal and inspect during commissioning.
- Keep cell access possible for inspection without dismantling the whole module.

## Links

- Checklist section: [10. Cell Compression and Internal Pack Mechanics](../build-readiness-checklist.md#10-cell-compression-and-internal-pack-mechanics)
- Diagram: [module physical layout](../diagrams/module-physical-layout.mmd)

