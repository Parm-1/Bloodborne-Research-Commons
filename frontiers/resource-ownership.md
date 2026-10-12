# Frontier — engine-owned resource identity and lifetime

## Question

Can existing publicly described GX registry work help identify a naturally reached Bloodborne resource's *logical producer, content authority, consumers, and safe retirement point* in another port?

## Known public inputs

- [RC-0001](../claims/RC-0001-gx-resources.md) — bbhost declares resource IDs, write sequence and overlap checks.
- [bbhost rendering architecture](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/rendering.md) — PROJECT_REPORTED: bbhost hooks GX's draw, dispatch, resource-creation and state methods and is moving from decoding GPU packets toward engine-level draw inputs.
- [bbport research snapshot](../sources/projects.yaml) — a separate runtime that, per its README, uses a renderer derived from shadPS4 with its own texture-set memoization and caches. No bbport equivalent of the bbhost registry was inspected, so whether the two share an identity notion is UNKNOWN.

## Missing facts

Natural game producer/consumer for a selected operation; coverage of all writes and aliases; guest-versus-host version relation; completion and failure; whether data is required after scene transition; chosen hardware, format and build. No source-only header establishes these facts automatically.

## Small candidate investigation

Compare the game-owned resource id and write sequence (RC-0001's `id` and `write_seq`) against the current selected cache object's version in permitted source/review records, then propose one distinct positive and one stale-address/reused-storage contradiction. Do not run a game or create a broad tracer solely from this document. An honest result may be that the current evidence cannot bind the two identifiers.
