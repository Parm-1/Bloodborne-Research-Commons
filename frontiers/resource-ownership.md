# Frontier — engine-owned resource identity and lifetime

## Question

Can existing publicly described GX registry work help identify a naturally reached Bloodborne resource's *logical producer, content authority, consumers, and safe retirement point* in another port?

## Known public inputs

- [RC-0001](../claims/RC-0001-gx-resources.md) — bbhost declares resource IDs, write sequence and overlap checks.
- [bbhost rendering architecture](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/rendering.md) — author descriptions of above-GNM draw/resource direction.
- [bbport research snapshot](../sources/projects.yaml) — separate runtime and cache machinery, not inherently the same identity system.

## Missing facts

Natural game producer/consumer for a selected operation; coverage of all writes and aliases; guest-versus-host version relation; completion and failure; whether data is required after scene transition; chosen hardware, format and build. No source-only header establishes these facts automatically.

## Small candidate investigation

Compare game-owned resource IDs/generation against the current selected cache object's version in permitted source/review records, then propose one distinct positive and one stale-address/reused-storage contradiction. Do not run a game or create a broad tracer solely from this document. An honest result may be that the current evidence cannot bind the two identifiers.
