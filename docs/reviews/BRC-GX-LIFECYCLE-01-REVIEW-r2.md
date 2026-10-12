# BRC-GX-LIFECYCLE-01 independent affected review r2

Frozen 2026-10-12. Same uninvolved reviewer as r1. This is an affected recheck, not a repetition of the unchanged lifecycle audit. No candidate authorship, fix design, source execution or acceptance action.

## Identity and result

Commons successor commit `9f67163b468ffdc71ada998acb2b0843c0160f68`, tag `brc-gx-lifecycle-candidate-r2`, tree `458d5e8f2a71f41ea450c56ce643a2c7609e10dd`; dossier `knowledge/gx-resource-lifecycle.md` blob `37c202a05743099b9db76a6538180e800f336d18`. Predecessor is frozen r1 `22a6991f433249dcdf10d02596c81977c1773182`. Exact upstream remains `droogie/bbhost` commit `566184a74f071166299bb656c4af479e5bbe2771`.

Prior frozen report `BRC-GX-LIFECYCLE-01-REVIEW-r1.md`, SHA-256 `f1081dc0468b49b5c80e29d5688fb9ba633cde685007d934541c156cb93de574`, remains unchanged. R1 contains the full independent identity checks, source-path assessment, limitations and issue-acceptance coverage. This report links that scope to the exact successor delta.

**F1 and F2 are resolved. No outstanding consequential finding from this affected review.** The retirement wording clarification is supported. RC-0004/0005/0006 remain supported at SOURCE_INSPECTED scope with the r1 limits. Original game layout/ABI assertions remain PROJECT_REPORTED. No runtime/game/native qualification, original-ID uniqueness, natural error schedule or upstream bug claim was added.

Technical acceptance, publication, separate fresh-reader dispatch and eventual editorial merge remain with their previously assigned owners. This review does not accept for them or authorize any external action.

## Changed contract and evidence checked

**F1 — zero-ID producer-to-consumer distinctions.** R2 explicitly separates masked original resource ID zero from missing host object IDs. Resource registration has no zero-ID rejection; lookup of an absent/null object returns zero. New bounded insertion failure supplies no new table entry; same-address re-registration instead replaces its slot ID with the next counter value. Enabled word-check mismatch returns zero. A resolved renderer image with a nonzero selected ID calls `texture_view_by_id`; zero calls descriptor-word `texture_view`. R2 correctly avoids saying either route guarantees a non-null view, and preserves the unknown wrap/immutability premises.

Source-faithful positives/negatives: readable fields with resource ID zero still register; nonzero host ID selects the ID route; absent host ID selects the word route. Existing-table re-registration is distinct from absence. Checked mismatch selects zero only when the optional check runs and has a creation hash. These conditions were inspected against source, not exercised as fixtures.

Checked bodies: [register/mask](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L252-L299), [object insertion/re-registration](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L184-L209), [lookup zero returns](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L797-L823), [optional word check](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gx_trace.cpp#L974-L997), [actual renderer selection](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/render.cpp#L8558-L8578). Interactions with the word memo and ID memo were reread at [textures.cpp:2672–2788](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2672-L2788); the text preserves word verification versus ID/flags/epoch assumptions.

**F2 — failed reads followed by retained-key dispatch.** R2 now states the return from `register_holder` occurs before replacing an old record, and the later caller receives no success result. It searches the chosen key, can update a retained type-2/3 record's T#, copy it and call `create_ahead`. The absent-key control is explicitly different from the retained-key control. Ahead queueing still requires the old type/initial-data/nonzero-memory fields, captured T#, enabled ahead and capacity. The text restricts this deduction to the specified non-1D path and does not generalize past the 1D key recomputation or claim a natural stale upload.

Raw conditional outcomes checked: failed field read plus absent later key yields no record/ahead call; the same failure with an eligible retained key permits later dispatch. A nonzero creation error count is not a registration-success predicate. A readable original resource ID of zero does not defeat ahead eligibility. This distinguishes field-read observation, registry phase and caller/queue phase.

Checked bodies: [registration early return and replacement](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L252-L299), [full result handling/caller](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L613-L683), [ahead eligibility/queue](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L340-L367). No self-checker flag substituted for these branches.

**Retirement wording.** Replacing “live-range retirement recheck” with “current-range coverage recheck at retirement” accurately matches [surface decision](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3316-L3339) and [lookup](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L882-L896), which has no explicit `alive` test. It does not alter the actual implementation contract or promote coverage into allocation retention.

## Delta checks, limits and continuation

Git independently confirms only the dossier changed: 24 insertions/7 deletions. Every other candidate path is byte-unchanged from r1, including claims, source registry/inventory, frontier, Director draft and historical reviews. The 17 blob rows match their r1 bytes; independently established public-source identities from r1 are reused. Candidate and source checkout are clean at their declared pins.

Changed dossier encoding passes UTF-8/no BOM/NUL/CR and Git whitespace checks. The four changed source URL locations exist and have valid extents at the exact pin. Independently counted corpus totals: 24 text files, 97 pinned citation occurrences, 82 distinct locations; 15 conditional table cases. Relative links are unchanged, so the r1 result of 108 links/9 anchors is reused. No new full-tree source audit, YAML parse, HTTP resurvey, comprehensive secret scan, fixture or game test is claimed. These mechanics bind locations and preservation, not truth.

The one next question remains unchanged: what producer-side ordering retains the same guest allocation identified by `TexturePrep::src/base/total_src` through the last guest read, including hash-only prep? R1's missing-allocation-ordering limit and positive/falsifying/UNKNOWN branches remain applicable. The dossier grants no experiment.

Allowed final mechanical integration remains verbatim copying/linking of the frozen r1/r2 reports, exact successor/review references, and status text naming this source-only review. That does not require another review ladder. The separate fresh-reader exercise using the published PR and the parent's publication/acceptance are still pending. Semantic additions beyond this reviewed delta require proportionate affected review; unchanged inventories need not be rebuilt.

No candidate/canonical edits, source import/execution, target/native/game operation, external write, host mutation, child dispatch or authority change occurred. Only this reviewer-owned successor report was written, once. No live process/tool handle exists; original author retains documentation ownership. Review/repair/integration token usage and whole-review elapsed time are unmeasured/unknown; no timed experiment occurred. No private project evidence or memory was consulted in this affected recheck.
