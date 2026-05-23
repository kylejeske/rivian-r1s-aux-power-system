# Decision: Module Fuse and Disconnect

Status: accepted
Date: 2026-05-23

## Context

Each removable module needs local positive-side fault protection and a manual way to isolate the module before unplugging the SB120 connector.

## Decision

Use a 60A Class T fuse per module, located as close to pack positive as practical.

Use a Blue Sea 6006 battery switch after the fuse as a manual service disconnect. Treat it as a no-load isolator, not a normal load-breaking switch.

## Open Questions

- Confirm final fuse holder packaging once the module enclosure layout is drawn.
- Confirm exact insulated covers/boots for fuse holder and switch studs.

## Evidence

- Littelfuse JLLN060 is a 60A Class T fuse with high DC interrupt rating.
- Class T provides better short-circuit interrupt margin than compact terminal fuses.
- Blue Sea 6006 has high carry rating, but low switching rating compared with its continuous rating, so use it only after loads and chargers are off.

## Consequences

- Module positive path becomes: pack positive -> 60A Class T fuse -> Blue Sea 6006 service disconnect -> SB120 positive.
- Module removal requires a no-load service sequence.
- Fuse replacement must be accessible without unpacking the cell stack.

## Links

- Checklist section: [4. Module Fuse, Disconnect, and Fault Protection](../build-readiness-checklist.md#4-module-fuse-disconnect-and-fault-protection)
- Structured data: [components](../data/components.json)

