# Decision: Dock Input Protection

Status: accepted
Date: 2026-05-24

## Context

Each battery module has an internal 60A Class T fuse. The dock still needs per-input protection because two modules can be paralleled on the common bus and one module/common bus can backfeed a fault on the other input path.

## Decision

Use one Blue Sea 285-Series 60A DC breaker on each dock module positive input.

Keep the internal module 60A Class T fuse. The dock breaker does not replace module-level fault protection.

## Open Questions

- Confirm exact Blue Sea 285-Series part number once mounting style is chosen.
- Confirm breaker placement in the dock physical layout.

## Evidence

- 60A aligns with the module fuse and 50A module operating target.
- Breakers give dock-side service isolation for each module input.
- Module Class T fuse remains the high-interrupt protection close to the cells.

## Consequences

- Each module can be isolated at the dock before plugging/unplugging or troubleshooting.
- Dock positive path becomes: module SB120 positive -> 60A dock input breaker -> positive busbar.
- Main dock output protection is still handled separately.

## Links

- Checklist section: [5. Dock Input Protection and Bus Architecture](../build-readiness-checklist.md#5-dock-input-protection-and-bus-architecture)
- Structured data: [components](../data/components.json)

