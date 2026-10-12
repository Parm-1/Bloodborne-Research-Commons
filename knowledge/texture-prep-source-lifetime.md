# Texture preparation: guest allocation, reads and completion

**Work:** BRC-PREP-OWNERSHIP-01, candidate r2, 2026-10-12. **Level:** SOURCE_INSPECTED, with conditional source reasoning and explicit UNKNOWN original-producer facts. The uninvolved [r1 source review](../docs/reviews/BRC-PREP-OWNERSHIP-01-REVIEW-r1.md) found no actionable finding; the parent accepted that source/documentation scope. Fresh-reader validation remains pending. The complete commission is [issue #3](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/3). This follows the accepted [GX lifecycle dossier](gx-resource-lifecycle.md) at Commons `1008f0b10f132dfe29859e5309a819d3af8150ab`; that dossier and its frozen reports remain unchanged.

**Result:** the public implementation orders CPU staging preparation before its recording is submitted. It does not make that wait a prerequisite for guest unmap/release or original GX allocator reuse. GPU-route hash-only preparation has a separate completion boundary: its pool state or an actual `wait` proves its reads finished; Surface erase and a successful GPU fence do not. The precise remaining fact is the original texture allocation owner's rule preventing removal/reuse, and ordering permitted writers, until these host readers finish. This is not an actual game failure or a requirement that every reader see one immutable snapshot.

All upstream citations below bind `droogie/bbhost@566184a74f071166299bb656c4af479e5bbe2771`. This is the x86-64 hook adapter and Vulkan implementation, including its Linux/Windows branches. No source script, fixture, native code, GPU work or game was executed. [RC-0007](../claims/RC-0007-prep-completion.md) and [RC-0008](../claims/RC-0008-map-removal-ordering.md) isolate the new implementation claims. The following table names actual reads, rather than inferring their phase from an object name.

## Producer, read, owner and completion

| Route / producer | Guest read endpoint | What is retained or ordered | Completion and missing allocation premise |
| --- | --- | --- | --- |
| CPU async: `upload_surface` copies `src/base/total_src`, layout and extents; submits prep and inserts it into `g_batch_preps` | `run_prep` untiles each selected level/slice from `src`, then performs sampled/whole content hash and exact whole-span hash from `base`; last guest read is in the second hash | Queue/worker, Surface and batch shared pointers retain the prep; batch/slot staging holds its destination. Pool mutex claims state 0 once, finishes state 2 after reads | `textures_before_submit` waits every batch prep before GPU submission. This orders destination consumption; guest producer must retain/read-enable its original allocation until those reads end. [upload][prep][batch][submit] |
| CPU inline (async disabled or check/probe path), and successful GPU mode-2 CPU comparison allocation | Same `run_prep` guest reads, synchronously before returning from that call | Caller holds prep; it assigns resulting hashes immediately. This local call needs no pool wait; state 0 here is not a queued unfinished job | Later destruction on that same sequential call path is after its reads. A concurrent producer still requires applicable synchronization; render mutex is not the kernel map mutex. [upload][prep] |
| GPU upload's hash-only job (also when mode-2 CPU comparison staging fails) | `content_hash_of(base,total_src)` followed by its exact=true call; no CPU untile destination | Pool queue/worker and, while attached, Surface retain prep. **No insertion into `g_batch_preps`** | Worker state 2 / `PrepPool::wait`, including `settle_prep`, proves completion. Submission and its fence have no dependency on this job. After Surface reset/erase no Surface `settle_prep` remains for this old job. [upload][prep][batch][settle] |
| GPU untile directly from import: `gpu_untile_plan` uses `guest_device_address` | Recorded compute dispatch reads imported source addresses; host recording is not the read | Pass copies source device address. Direct-memory imports use mirror backing and persistent import ownership; destination staging/image follows command barriers and slot rules | Successful completion of the relevant submitted GPU work bounds that GPU read, independently of hash-only completion. Original owner must order allocation reuse and permitted writes through that read. See import boundary below. [plan][gpuuntile][device][imports][fence] |
| Device-local GPU route (`in_vram`) | Transfer `vkCmdCopyBuffer` fetches `sf.total_src` from `vram_src`; subsequent untile reads scratch, not original guest bytes | All-commands write-to-transfer-read barrier precedes fetch; transfer-to-compute barrier follows it; scratch/staging belongs to the recording/slot | Guest-source obligation ends at fetch completion, not necessarily all later image work. Slot fence is a conservative completion endpoint for submitted fetch; no CPU hash dependency follows. [gpucommands][submit][fence] |

`content_hash_of` uses raw host memory reads; nonexact spans above 256 KiB are sampled, while exact=true reads the whole span. It does not perform a mapping check inside the hash. `run_prep` hashes even if untile returns false and zero-fills its destination. The two hashes and untile are successive reads, not one atomic capture. [hash][prep]

## What the pool and Surface lifecycle actually guarantee

`submit` appends a shared pointer under the pool mutex. A worker removes it and claims state 0 as 1; `wait` can claim a still-queued state-0 prep itself, unlock, run it, relock and set 2. A worker later encountering that queue entry skips its nonzero state. A waiter on state 1 waits for 2. Therefore a supported normal wait cannot return while that prep's `run_prep` is still reading. The queue may retain an already completed prep until it pops the skipped entry; object destruction is not the read endpoint. [prep]

`settle_prep` waits, copies hashes and drops the Surface pointer. In contrast, `upload_surface` first resets the old pointer, before mapping/staging failure checks; a refresh can supersede its hashes while the earlier upload still runs. The watch-dirty refresh branch calls upload without first settling. The hash-comparison branch, after cadence/registration/mapping gates, returns while prep is unfinished and settles only a finished one. These are different behaviors, not a universal wait-on-refresh. [settle][upload][refresh]

Descriptor replacement copies the old Surface locally, defers views/image, and erases it; `note_surface_erased` updates occupancy/index accounting, not prep state. Due retirement, cold eviction, return from host memory and reused shader-written Surface removal likewise defer objects and erase records without a prep wait. CPU async jobs still have batch ownership and submission wait; hash-only jobs still have queue/worker ownership but no batch wait. An erased Surface's old hash job can finish, but its resulting hashes have no attached Surface consumer. These inspected erase paths contain no cancel operation. [replacement][erases][batch][accounting]

Neither pool nor ahead worker implements a stop flag, cancellation acknowledgment, drain/join or shutdown method: they are detached infinite loops. Reset is not cancellation of a queued/running prep. This source gives no general orderly shutdown receipt for their guest reads; process exit is not a successful completion observation. GPU submit/device-loss code can drop a recording after the CPU batch wait, and failed/stuck fence handling preserves GPU resources without normal successful retirement. Neither path waits the hash-only queue. Scope is these worker/submit bodies, not every possible process termination. [prep][ahead][submit][fence]

## Allocation owner and writer candidates followed

**Mapping lock.** `hle_kernel_va_mapped` checks a thread-local mapping snapshot keyed by `g_maps_gen`; rebuilding snapshots briefly holds `g_dmem_mu`, then returns. Its false result prevents starting this upload, but its true result does not pin mapping readability, physical identity or later lifetime. It deliberately requests mapped, not CPU-readable coverage. `hle_kernel_write_watch` holds `g_dmem_mu` through direct read/write/nonexecute coverage and watch arming only. Neither scope extends through `run_prep`. [maps][watcharm]

**Removal and replacement.** `maps_cut_locked` edits/splits map records, advances generation, forgets watches and calls `gx_resources_memory_released`. `unmap_range` cuts CPU and applicable GPU aliases under `g_dmem_mu`, then calls host unmap outside the lock. `hle_release_direct` removes physical allocation accounting under that mutex and subsequently unmaps victim CPU mappings; flex release calls unmap. Exact mapping can replace old records after host mapping. None of these bodies enters the prep pool or waits its read endpoints. These adapters contradict an unconditional claim that *kernel removal itself* waits preparation; whether the original caller permits the overlap remains UNKNOWN. [cut][release][mapreplace]

**GX texture owner.** Public header comments identify holder reference count +0x10, memory allocator at resource +0x18 and allocator free slot +0x70, with deleting destructors 0x256d1a0 / 0x256d310 (PROJECT_REPORTED original layout). The inspected destructor entry adapter unregisters, releases whole-page watches and queues host texture retirement with current submitted CP total, then returns to the displaced original destructor. It does not take a guest reference or wait prep before the original free. `gx_resources_memory_released` invalidates indexed records and queues retirement; this is notification, not delayed host unmap. The adapter does not supply the original allocator free/recycle body. Ring 0x2adb1b0 is trace-only, not a texture retention barrier. [owner][dtor][retire][memoryrelease]

**Game job barrier and other allocator.** Source comments say a game job barrier waits for GX-thread draw snapshots/fingerprints. Those comments do not publish that barrier's implementation or extend it to detached ahead/PrepPool workers. The CP `Job` owns optional command-buffer byte snapshots, not texture bytes. Its `done` callback follows the job's submit/flush choice and precedes retired-counter publication; the callback body is supplied by a caller, not an allocation token carried by prep. [gxbarrier][cpjob][cpend]

The applicable tempting allocator candidate was followed: `decomp/gx/block_reclaim.cpp` wraps the original resource-table block reclaim (0x2aaa860), invokes the original function, and on a particular empty-pool path flushes recorded GPU work, then may wait CP totals and retry. This covers blocks containing draw T#/S#/V# tables, not the texture allocation sampled by prep. Original calls and source comments are not proof of that original function's behavior. `gnm_exec.cpp`'s optional early arena free applies CAS 2→0 to command-arena markers after a job walk; it is disabled by default and does not retain a TexturePrep source. Neither candidate can be promoted into the missing texture allocator contract. [reclaim][arena]

**Writes/coherence.** `textures_retired(slot)`, reached after successful slot retirement, finds the current Surface by writeback base and checks mapped coverage. It tiles writeback staging into that Surface's current raw guest pointer **before** `settle_prep(sf)`; only if tiling succeeds does it wait/settle and recompute both hashes. Thus that wait orders the later rehash, not the preceding guest writes against a still-running hash-only prep. Missing Surface/mapping skips the writes; failed tiling skips settle/rehash (possibly after earlier slices were written). The permitted sampling relation and actual overlap remain UNKNOWN; this host writer is not an original-producer snapshot promise. [writeback][fence]

A write watch makes pages writable on fault and records a dirty sequence so a later eligible bind can refresh. Release/forget also mark changes. It does not freeze the bytes until prep finishes. Other mappings and CP/GPU writes are explicitly separate refresh considerations. A Map sequence is not a completed-write barrier. Nothing inspected ties sampled hash, exact hash and GPU/CPU upload to one allowed content version. That is a question about the producer's permitted sampling interval, not proof that immutable snapshot semantics are required. [watchfault][watchforget][refresh]; prior [Map finding](gx-resource-lifecycle.md#creation-map-and-lookup).

## Direct imported GPU-memory boundary

`guest_device_address` checks coverage, rebuilds mapping/page tables and requires the span within one mapping/import. It returns 0 on failure, which declines the GPU plan and can select CPU preparation; it does not pin the allocation. `locate` supplies buffer/offset/available span for device-local fetch. Successful direct-memory imports are appended to `g.dmem[index].imports`; the GPU mirror is a distinct whole-backing mapping, so kernel removal of a guest VA is not removal of that mirror/import. This resolves one candidate host-object lifetime mechanism, while leaving original physical suballocation reuse and content authority unresolved. [device][locate][imports][mirror]

The flexible branch imports a host pointer and caches by base VA. Its mapping backing/remap lifetime and Vulkan external-memory-host requirements have not been qualified by this inspection. **Stop this branch at the exact dependency:** `gpu.cpp::import_anon/rebuild_page_tables` and kernel flexible map/unmap interaction must establish that imported host pages remain valid through the selected GPU read, including same-VA replacement. Persistent cache membership alone is not that proof. No universal alias or Vulkan API correctness claim follows. The inspected GLSL read describes intended addresses; compiled SPIR-V equivalence, driver behavior and runtime execution are untested. [anon][pagetables][shader]

## Source-faithful ordering cases (reasoning only)

A and B below mean hypothetical original allocations, not registry IDs used as ground truth. These cases use raw premises and control-flow guards; no synthetic C++, GPU or game experiments ran.

| Case / raw premise | Order and guard | Supported result / meaningful negative |
| --- | --- | --- |
| P1 CPU async positive | A is readable/mapped; CPU route selected; original owner keeps A and permits no intervening writer through untile and both hashes. State 0 claimed by worker; state 2; batch wait; submit; owner later frees A | Pool/batch ordering makes staging ready; under the stated owner premise allocation and content agree. The premise is not inferred from pool state. |
| P2 waiter/inline positives | Same retained-readable A; queued state 0 is claimed by waiter, or worker state 1 is joined; separately nonqueued inline call returns before later same-thread free | `wait` ends after reads in both pool cases; inline call ends locally. A nonqueued inline prep's state 0 does not falsify that completion. Concurrent free is excluded only by the premise. |
| P3 GPU/hash positive | Owner retains A through transfer/compute source reads **and** exact CPU hash end; prior applicable GPU writes are ordered by the recorded fetch barrier | Supported command ordering and separate pool completion can both succeed. GPU completion may precede hash completion; same-version hashes/upload need the producer's allowed writer interval. |
| N1 initial mapping/staging failure | Coverage false at upload check, or staging allocation fails before prep construction; old `sf.prep` already reset | No new prep submitted on that failure. Old queued/running prep is not canceled; failure does not prove all reads stopped. Mapped-but-unreadable is not rejected by the mapped check. |
| N2 conditional unmap overlap | Successful A check; queued state 0 or running state 1; another caller executes unmap/release before final hash | Inspected removal bodies do not join prep. Reads may lack valid original memory under this ordering; no source guard there rejects it. Original caller ordering/reachability is UNKNOWN, not an observed crash. |
| N3 same-address replacement | A saved raw base; A retired and B occupies that base before worker/hash; mapping/current GX coverage true for B | Those checks can pass for B; old raw fields still read that address. No proof of old identity/content. Compatible reuse may be permitted by an unknown producer contract; a new ID's existence alone does not make it a bug. |
| N4 descriptor/content change | Shape replacement erases Surface or dirty-watch branch resets old prep while it is state 0/1; relevant writes alter bytes during untile/hash | Captured old layout is retained; CPU batch still waits old staging work. Hash-only has only pool ownership. Watch can trigger later upload but does not make successive reads one version or cancel old work. |
| N5 hash-only Surface erased after GPU submit | Hash prep remains state 0/1; due retirement or replacement drops Surface; relevant GPU fence signals | Fence/erase proves no CPU hash completion. Only old prep state 2 / actual wait, or a demonstrated original producer barrier covering it, answers whether its original allocation is no longer read. |
| N7 host writeback | Current Surface and mapped guard pass at slot retirement; tiling writes guest bytes while an attached hash-only prep could be state 0/1 | `settle_prep` follows writes on successful tiling, then rehashes. It is not a before-write join; absent mapping/Surface rejects writes, failed tiling skips the join/rehash. No game overlap or forbidden-version requirement is established. |
| N6 error/cancel/shutdown | Unsupported CPU untile; GPU import/plan failure; mode-2 comparison allocation failure; failed fence; attempted reset/exit | CPU zero-fill still hashes; GPU decline may fall back to CPU; comparison failure can queue hash-only; failed fence is not successful GPU retirement; reset/exit supplies no pool cancellation/drain receipt. |

## Bounded decision and stop rule

The route-supported staging guarantee is resolved. Kernel/GX removal adapters do not implement a prep completion barrier; the contrary unconditional claim is contradicted at that adapter scope. Actual game allocation ordering remains **UNKNOWN**: the unavailable original texture allocator/free/reuse and job-barrier relation must identify whether A stays readable and authoritative through (1) CPU untile plus final exact hash, (2) hash-only final exact hash even after Surface erase, and (3) GPU original-source fetch/compute completion. It must also name which producer writes may occur during each interval. The public hook comments and unrelated table/arena allocator cannot supply that fact.

**One next decision:** accept this as the completed source-research checkpoint and keep adaptation at KNOWLEDGE_REFERENCE until a publicly inspectable original texture-owner ordering contract becomes available. That new fact would warrant a focused recheck; no implementation or mandatory runtime campaign is selected. Stop here: no public original producer body inspected establishes the missing relation, and the flexible import branch has its exact separate subsystem boundary.

**Reuse/origin:** KNOWLEDGE_REFERENCE. Upstream authorship is droogie/bbhost, declared GPL-3.0-or-later by its README/LICENSE; third-party/per-file exceptions remain as recorded in [source registry](../sources/projects.yaml). No upstream code imported and no license change. Commons original documentation retains CC BY 4.0. This dossier proves source control flow only, not original ABI fidelity, physical-alias coverage, game reachability, gameplay corruption, measured performance or runtime safety.

## Inspected source identity and author checks

The table binds decisive files actually inspected in this stage, including relevant complete function bodies and callers. It is not a claim to have read each whole file. Unchanged accepted GX inventory/check receipts are reused; this focused table does not rebuild that inventory.

| Public upstream path | Git blob SHA-1 |
| --- | --- |
| src/host/textures.cpp | 54b61d74e06a3c124661b97aa58f092950befbab |
| src/hle/kernel.cpp | 8c2e25d7cf980a04ebc61e9f05c2bf6ebfe4c22c |
| src/host/gpu.cpp | 0ad2859af2ae5f81ef641018c87c29735a507203 |
| src/host/gpu_internal.h | 31657a3a0a95e852e306296cc7feec0f9ee70a91 |
| src/host/gpu_untile.cpp | 37d9be37bbae225cc5d7c3396b1e6be40586dd7c |
| src/host/shaders/untile.comp | a424925f33ee84e65324f1a8d9079d5a5eb36c64 |
| src/engine/gx_resources.cpp | aca314bb5dd768ea24076279a0d25e821d201365 |
| src/engine/gx_resources.h | f6edcb582e141aabfa30384e381fb79f10e9653c |
| src/core/write_watch.cpp | fb6876917ca9cd454dd211db8688fa7a6e896a9a |
| src/engine/gx_state.cpp | ee0bf457f59a7b08e54bba9ec6237129a9f6fecd |
| src/hle/gx_trace.cpp | c1bf02a6d77a5ec0285320f0a6cc7cc85166ea31 |
| src/hle/gnm_exec.cpp | ca2c289e6b03f6436dcb7540dc21107ba7cdfb0e |
| src/decomp/gx/block_reclaim.cpp | f651867f3f80b047ab572f48aa654b3b93406416 |

Author validation and resource closure are frozen in [r1 author report](../docs/reviews/BRC-PREP-OWNERSHIP-01-AUTHOR-r1.md). The completed [r1 source review](../docs/reviews/BRC-PREP-OWNERSHIP-01-REVIEW-r1.md) is preserved verbatim in r2. Author usage and elapsed time are not measured; no billing inference. There are no live author execution/process handles or children. Public push/PR and final acceptance remain with the parent.

## Candidate r2 review integration

The parent accepted r1 `26575ec77d342e78a266207a12e3bf45b1951cc3`, tree `e76e1c3b4bb73cbd8fcaed12a2ba9b7686ec911e`, dossier blob `a24af45aafb9af94eef5247c0a40b324bdb76491`, after the uninvolved Sol/high reviewer `prep_ownership_review` found no actionable source-semantics or acceptance-coverage defect. The review independently followed allocator admission/release, CP callbacks/backpressure and the decisive reader/removal edges. R2 copies the report verbatim, SHA-256 `a06767351e96725ad3dbc8703f3c008f60c4eb48c6d93c277d8a98a7cb01760f`, and updates review/status records only. All technical bodies, source pins/blobs, ten reasoning rows and original-producer UNKNOWNs remain unchanged. The accepted GX dossier, earlier claims/reviews, Director draft and frozen AUTHOR-r1 remain byte-identical. Earlier pending statements in frozen r1 records describe their original date; r2 does not rewrite them.

Focused r2 checks: seven changed/added texts pass UTF-8/no BOM/NUL/CR, Git whitespace and bounded public-path/credential-prefix checks with zero reported errors/hits. Six added relative links resolve, with no new anchors. The copied review matches its frozen bytes/SHA-256; technical sections, source identity table and pinned citation definitions match r1. Unchanged 13-source-blob and source-location receipts are reused without inventory rebuild, source fetch or HTTP resurvey. Fresh-reader validation and public PR delivery remain pending downstream. No runtime tests or external writes occurred, no live handles/children remain, and author usage/elapsed time are unmeasured.

[hash]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L634-L676

[prep]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L823-L940

[settle]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L968-L977

[upload]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1051-L1151

[plan]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1010-L1047

[gpucommands]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1155-L1199

[batch]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3295-L3351

[refresh]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1712-L1865

[replacement]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2445-L2480

[erases]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3390-L3505

[accounting]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1340-L1353

[maps]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L712-L800

[watcharm]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L476-L500

[cut]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L327-L471

[release]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L1013-L1053

[mapreplace]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L918-L982

[owner]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L4-L16

[dtor]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L504-L538

[retire]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L369-L415

[memoryrelease]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L859-L880

[ahead]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L308-L367

[gxbarrier]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gx_trace.cpp#L1917-L1940

[cpjob]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gnm_exec.cpp#L2096-L2126

[reclaim]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/decomp/gx/block_reclaim.cpp#L74-L108

[arena]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gnm_exec.cpp#L754-L807

[watchfault]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/write_watch.cpp#L260-L309

[watchforget]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/write_watch.cpp#L489-L507

[device]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L6485-L6509

[locate]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L1308-L1349

[imports]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L404-L447

[mirror]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L632-L642

[anon]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L624-L678

[pagetables]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L1041-L1064

[gpuuntile]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu_untile.cpp#L65-L72

[shader]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/shaders/untile.comp#L94-L101

[submit]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L5197-L5235

[fence]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L4180-L4247

[cpend]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gnm_exec.cpp#L2281-L2297

[writeback]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3528-L3562
