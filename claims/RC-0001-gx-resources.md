# RC-0001 — bbhost exposes a GX resource registry interface

**Level:** SOURCE_INSPECTED (public header), 2026-10-12. **Game behavior in another port:** UNKNOWN.

At bbhost commit `566184a74f071166299bb656c4af479e5bbe2771`, `src/engine/gx_resources.h` declares resource IDs, lifetime/written-state fields, address-based lookups, overlapping-newer-resource checks, and release/protection notifications. The comments describe holder and memory relationships and the tracking of creation/Map writes.

**Source:** [exact public header](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h).

**Important limits:** Interface descriptions are not proof that hooks cover all naturally reached game creations, GPU writes, physical aliasing or delayed consumers. Inspect implementation, missed-event paths, identity reuse/wrap and actual tests before adapting it. A bbport cache UID must not be relabeled as a game-owned GX identity.

**Next testable question:** Identify one actual game-reached GX producer + consumer and a negative involving alias/reused storage to establish whether the claimed registry generation corresponds to the selected resource lifetime.
