# RC-0001 — bbhost exposes a GX resource registry interface

**Level:** SOURCE_INSPECTED for the declared interface (public header). PROJECT_REPORTED for the header comments' statements about the game's own GX internals (object layout, id counter, id reuse), which are the author's reverse-engineering claims and are not checked here. **Game behavior in another port:** UNKNOWN. **Independently reviewed:** not yet.

**Checked:** 2026-10-12, header read in full at the pinned commit; blob `f6edcb582e141aabfa30384e381fb79f10e9653c` (git SHA-1 of the file bytes).

At bbhost commit `566184a74f071166299bb656c4af479e5bbe2771`, `src/engine/gx_resources.h` declares (declaration only; the implementation was not inspected):

- a `GxResourceInfo` record with id, type (1 buffer, 2 1D, 3 2D, 4 3D), usage, guest memory address, byte size, `write_seq`, `initial_data`, `alive` and `created_flip`;
- lookups by guest address range: `gx_resource_at` (the live resource whose memory covers the range) and `gx_resource_newer_overlapping` (a live resource created after a given flip that overlaps the range);
- notifications that guest memory was unmapped (`gx_resources_memory_released`: resources lying there are treated as dead whether or not a holder object still exists) and that its protection changed (`gx_resources_memory_protected`: counted for covered resources);
- a write sequence the comments say advances on creation with initial data and on every Map, used by the texture cache to decide whether GX wrote a surface since the cache last uploaded it;
- separate id registrations for shader and input-layout objects, render-target/depth views, shader-resource views and samplers.

The comments state, as author claims, that a resource made over the same memory later gets a new id (so the id is the identity and the address is only a lookup key) and that shader/input-layout object ids are never reused. They also record the header's own coverage gaps: an object created before the hooks, or when the table is full, has id 0, and the create-failure count is 0 when the registry is off.

**Source:** [exact public header](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h).

**Important limits:** Interface descriptions are not proof that hooks cover all naturally reached game creations, GPU writes, physical aliasing or delayed consumers. The comment addresses (for example `0x2565c10`) are executable-build specific and this header does not itself name the build. `created_flip` is not defined beyond its name in this header. Inspect the implementation, missed-event paths, identity reuse/wrap and actual tests before adapting any of it. An identifier or cache key from another port (for example a texture-cache key) must not be relabeled as a game-owned GX identity.

**Reuse disposition:** KNOWLEDGE_REFERENCE. bbhost is declared GPL-3.0-or-later ([source registry](../sources/projects.yaml)); no code is copied here.

**Next testable question:** Identify one actual game-reached GX producer and consumer plus a negative involving alias/reused storage, to establish whether the registry's id and `write_seq` correspond to the selected resource's lifetime and content authority.

## Revision notes

- **r1, 2026-10-12** (supersedes the wording of the seed commit; recover the original with `git show seed-original:claims/RC-0001-gx-resources.md`). The seed's facts were confirmed against the pinned header. Changes: split the level into SOURCE_INSPECTED (interface) and PROJECT_REPORTED (guest-internals comments); listed the declared fields and calls and the header's own coverage gaps; added the build-specific-address and `created_flip` limits; replaced "bbport cache UID" with a generic cache-key caution, since no bbport identifier was inspected; replaced "registry generation" in the next question, because the header has no field named generation (it has `id`, `write_seq` and `created_flip`); added blob hash, reuse disposition and review status.
