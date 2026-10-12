# BRC-GX-LIFECYCLE-01 narrow affected review r3

Frozen 2026-10-12. Same uninvolved reviewer; source-only review of the clarified refresh table predicate and its upload-return interaction. Unchanged contracts/inventories reuse the frozen r1/r2 reviews. No candidate authorship or fix design.

## Exact subject and result

Commons commit `54695ff00e3452d94df939b2c86021088e3897d4`, tag `brc-gx-lifecycle-candidate-r3`, tree `c61a63284e574daa33c5e1270dc7362cbafcabb1`, dossier `knowledge/gx-resource-lifecycle.md` blob `1aa7a9d21c35bf7ad9b7296ab88abd8439437080`. Predecessor `9f67163b468ffdc71ada998acb2b0843c0160f68` is the reviewed r2. Upstream remains `droogie/bbhost` commit `566184a74f071166299bb656c4af479e5bbe2771`.

**The qualified refresh row is supported. No outstanding finding in this narrow affected scope.** It establishes a source branch that calls census/upload, not successful upload, prep completion, fence completion or a guest allocation lease. SOURCE_INSPECTED/PROJECT_REPORTED levels and all r1/r2 limits remain unchanged. Parent owns acceptance/publication and the separate fresh reader; editorial merge remains with its appointed owner. This report grants no acceptance or external-action authority.

## Predicate and contradictory raw-field checks

The inspected function computes `stamp = g.record_serial + 1`. With `g_refresh_once` true and `sf.refreshed_serial == stamp`, it returns before testing the watch. Otherwise it passes that guard, updating the stamp when the option is enabled. The dirty-watch branch then requires `sf.watched && !sf.gpu_written` and nonzero `write_watch_dirty` result. Under those raw predicates it calls `census_upload(sf, "write watch")` then `upload_surface(...)`. R3 states these conditions and calls accurately. Descriptor compatibility is a context premise for the already selected Surface, not another invented guard inside this branch.

Contradictory conditions: the same recording stamp with refresh-once enabled prevents this branch even if the watch is dirty; `gpu_written` bypasses the watch branch; zero detected pages does not enter it. These negatives concern this branch, not universal absence of a later hash-driven upload. An advanced Map sequence is not tested by the branch and cannot replace its predicates.

The call to `upload_surface` ignores its Boolean return here. That callee can return false on missing mapped coverage or failed staging acquisition. Consequently calling it and updating census/log counters does not establish upload success. Its true return follows recording/update operations, not a successful Vulkan slot fence. The clarified row preserves that separation.

Evidence: [refresh configuration and complete watch branch](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1698-L1762); [census attribution/mapping branch](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1623-L1646); [upload mapping rejection](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1051-L1065); [staging rejection](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1090-L1104); [record/update/true return](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1230-L1240). These are inspected conditional branches, not executed fixtures or game observations.

## Integration checks and closure

Exact candidate/tag/tree/dossier pins and clean source/candidate state were read directly. The source pin remains the previously independently identified public source; no refetch or unchanged inventory rebuild was needed. The candidate delta confirms the refresh row is the only new technical wording, alongside status/history/link integration. Claim technical bodies and frontier technical body are unchanged; RC-0001 appends history while retaining its prior prefix. Both copied review files independently match their original bytes and SHA-256 values: r1 `f1081dc0468b49b5c80e29d5688fb9ba633cde685007d934541c156cb93de574`, r2 `060a1633f25ed3ba4e9abac4c0e5475376375a991915e90916631ccfb4babfc9`. Git whitespace check passes. Author-reported changed-text/link counts were not rebuilt in this narrow review; unchanged receipts retain their previous measurement scope.

Verbatim copying/linking of this frozen report and exact status updates naming this reviewed source-only predicate are permitted final mechanical integration without another review ladder. Any further semantic delta needs proportionate affected review. Fresh-reader exercise and public PR delivery remain outside this review. The selected next question stays bound to allocation ordering from `TexturePrep::src/base/total_src` queueing through the last guest read, including hash-only prep.

No candidate/canonical changes, source import/execution, target/native/game test, private evidence/memory use, external write, host mutation or child dispatch occurred. Only this reviewer-owned report was written once and frozen. No process or tool handle requires resuming; original author retains documentation ownership. Usage and whole-review elapsed time are unmeasured/unknown; there was no timed experiment.
