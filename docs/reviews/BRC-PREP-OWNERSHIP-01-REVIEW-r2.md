# BRC-PREP-OWNERSHIP-01 — affected independent recheck r2

Date: 2026-10-12. Reviewer: same uninvolved native Sol/high evidence reviewer `prep_ownership_review`. Linked predecessor: frozen [source review r1](BRC-PREP-OWNERSHIP-01-REVIEW-r1.md), SHA-256 `a06767351e96725ad3dbc8703f3c008f60c4eb48c6d93c277d8a98a7cb01760f`. R1 remains unchanged. This report is an affected source/documentation recheck, not parent acceptance or publication authority.

## Exact subject and trigger

- Candidate r3 commit: `0001cbd3cb00b961fd0d9201a2b51409198f89df`.
- Candidate tree: `634111b66300b08eab423a7ec0efbd53c629e3e5`.
- Dossier blob: `352f603c5023f3db30e3f5208d93580b7ec45daa`.
- Compared integrated/public r2: `f7a046b440834280ef9de32392947f0ebc8cdf2d`.
- Upstream unchanged: `droogie/bbhost@566184a74f071166299bb656c4af479e5bbe2771`.
- Fresh-reader report SHA-256: `4847b24d962b87346f390ebed91ddf025594728910ac2fe3d2832a4c2d01e04e`.

The parent reported acceptance of r1 source review and the fresh reader's precision finding, then the original author delivered the frozen r3 pins and activated this narrow recheck. The reviewer did not author or design the candidate repair. The actual trigger is the distinction between a source-defined same-job completion predicate and an available post-erase caller receipt. The original full source research is already reviewed; no new broad audit or fresh-reader exercise is commissioned here.

## Result

No remaining actionable finding in the r3 repair or its affected interactions. The new wording resolves the fresh-reader precision finding at the stated interface scope. It requires the same prep identity for state/wait observation, does not advertise a detached-job receipt, and does not infer allocation validity from completion. Parent acceptance and final report/status integration remain separate decisions.

The original raw guest allocation/writer/sampling UNKNOWN, CPU staging guarantee, hash-only versus GPU completion distinction and game/runtime exclusions remain unchanged. No observer implementation or stronger safety requirement is introduced. No ordinary repair activation is needed from this recheck.

## Decisive affected evidence

References below bind the unchanged upstream pin. Existing r1 source identities, full source scope and inventories are reused; only the affected edges were reread.

- `textures.cpp:823–940` defines raw guest `base/total_src`, reads both hashes in the hash-only path, and publishes state 2 only after `run_prep` returns. A queued state-0 waiter can run that job; a state-1 waiter joins that same job. The queue is a private member and a worker's shared pointer is local. Neither retention alone exposes a caller lookup or receipt. Positive: a caller actually holding the same prep can observe its state 2 or complete a wait. Negative: another job's state 2, a reused VA or aggregate activity does not identify this prep.
- `textures.cpp:968–976` requires a `TexturePrep` reference for `prep_done` and uses the attached `sf.prep` for `settle_prep`. `1051–1055` drops the old Surface pointer before coverage failure, while `1101–1151` creates/submits a new job and returns upload success rather than a per-job handle. Hash-only jobs are attached to Surface and pool, without CPU batch membership. Thus dropping the last Surface reference can leave pool/worker ownership without an exposed old-job observation in these paths. A new prep at the same base cannot substitute for retained job identity.
- `textures.cpp:3295–3351` retirement entries contain base/bytes/CP threshold, not the old prep; due erase does not join it. `textures_before_submit` waits `g_batch_preps`, which excludes hash-only work. Existing reset/erase facts and successful GPU-fence scope from r1 remain applicable. Conditional negative: old hash state 0/1 followed by Surface erase and GPU completion still gives no hash-completion guarantee or detached receipt.
- Newly cited `gpu_internal.h:1284–1300`, blob `31657a3a0a95e852e306296cc7feec0f9ee70a91`, declares texture source-span lookup, batch waits, upload/copy/carry operations and submission/retirement interfaces. These declarations expose no old hash-only prep handle/query/join receipt. A focused search of prep references in `textures.cpp`, `gpu_internal.h` and `gpu.h` corroborates the selected-interface scope; it is not a universal absence proof over every possible observer or future implementation.

The changed Result, route table, pool paragraph, N5 and RC-0007 correctly qualify identity and available observation. They also preserve the independent requirement that allocation readability/identity and permitted writes were valid during the reads: completion tells when this prep stopped, not whether its input lifetime had been safe. The new references point to the actual declaration range and existing producer/pool bodies. No runtime outcome or receipt was manufactured from this reasoning.

## Integration, preservation and mechanical coverage

The r2-to-r3 diff is limited to seven texts: dossier, RC-0007, RC-0008 status, frontier status, START_HERE, llms.txt and the added frozen fresh-reader report. Navigation/status accurately says the reader check completed with a precision finding, repair is present and affected recheck was pending at candidate freeze. The historical r2 integration record remains intact; the candidate does not already claim this repair was accepted.

Independently checked candidate commit/tree/blob pins, clean candidate/upstream worktree status, whitespace diff, unchanged prior accepted GX/report paths, and exact frozen report digests. The integrated REVIEW-r1 and fresh-reader report match their original temporary frozen bytes; AUTHOR-r1 retains SHA-256 `45f26c13ebef1ea69943ff1df58a68b0365939abda1c3d5dde25db47b35f2b03`. No edits to those reports or accepted GX artifacts appear in the diff. The author receipt's seven texts, five added relative links/no anchors and 27 other files preserved remain author mechanical categories; no repeated inventory/link-validation script was run or promoted to source proof.

## Limits, next consumer and closure

Only this own temporary report was written. Candidate, upstream scratch, frozen predecessor reports and canonical state stayed unchanged. All read commands finished; no process/session handle, runtime resource or child was created. No private project/memory evidence, script/native/fixture/GPU/game execution, external write/outreach, source import, host change or spend occurred. Usage and elapsed time are unmeasured; no billing inference is available.

Deliver this frozen result to the parent and original author. Parent alone accepts and commissions final r4 integration/publication; no changed authority or research contract is inferred from this no-finding recheck. A successor integrating this report must bind its own final commit/tree and preserve this report verbatim. The report digest is returned out of band after freezing, avoiding self-reference.
