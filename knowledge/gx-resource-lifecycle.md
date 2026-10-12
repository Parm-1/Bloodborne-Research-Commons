# GX resource lifecycle at the pinned bbhost implementation

**Work:** BRC-GX-LIFECYCLE-01, candidate r5, final reader-report integration, 2026-10-12. **Level:** SOURCE_INSPECTED for implementation; game layout, original ABI semantics and performance comments remain PROJECT_REPORTED. Source acceptance follows [r1 review](../docs/reviews/BRC-GX-LIFECYCLE-01-REVIEW-r1.md), [r2 F1/F2 recheck](../docs/reviews/BRC-GX-LIFECYCLE-01-REVIEW-r2.md) and [r3 refresh-predicate recheck](../docs/reviews/BRC-GX-LIFECYCLE-01-REVIEW-r3.md). The parent accepted r4 integration and the completed [fresh-reader result](../docs/reviews/BRC-GX-LIFECYCLE-01-FRESH-READER-r1.md) at [public r4 head](https://github.com/Parm-1/Bloodborne-Research-Commons/tree/273043492d41ac1a42cb3a7c069b31b68b974166), with no substantive correction. Acceptance remains implementation-source/documentation only; no source, fixture or game execution occurred.

An address that resolves and an advanced Map sequence establish a registry observation at two phases. They do not identify an older queued job's original resource, prove changed bytes, or establish safe retirement. The downstream implementation does supply safeguards: existing-surface refusal, descriptor-dependent replacement, content refresh, a current-range coverage recheck at retirement, and deferred destruction after a Vulkan fence. Their scopes differ; none turns the initial observations into an enduring guest-memory lease.

The complete public commission is [issue #1](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/1) and [PR #2](https://github.com/Parm-1/Bloodborne-Research-Commons/pull/2). The [Director draft](../docs/drafts/BRC-GX-LIFECYCLE-01-source-inspection.md) at Commons `22445011206afa47772461cf4ad35a9cdf8ebc48` is preserved unchanged. [RC-0001](../claims/RC-0001-gx-resources.md) keeps its earlier header-only provenance. The implementation findings are [RC-0004](../claims/RC-0004-map-observation.md), [RC-0005](../claims/RC-0005-ahead-consumer.md), and [RC-0006](../claims/RC-0006-deferred-retirement.md).

## Exact scope and source ABI

All upstream references in this dossier name `droogie/bbhost` commit **566184a74f071166299bb656c4af479e5bbe2771**. This describes its x86-64 guest hook adapter and Vulkan host implementation, including conditional Linux/Windows code; neither host was run here. The installer caller compares the image SHA-256 with the constant labelled the known 1.09 build before reaching `gx_resources_install`. That source gate is inspected; the game's build/layout correspondence is an upstream assertion, not independently measured. [runtime.cpp:335–391][runtime]; [addr.h:5–16][addr].

`GUEST_ABI` is `sysv_abi` on Windows and empty on Linux. The prologue emitter pushes rdi, rsi, rdx, rcx, r8, r9, making the saved array r9/r8/rcx/rdx/rsi/rdi/return address. Creator and Map hooks store those arguments in thread-local `Pending`, replacing the return address. `gx_res_ret` passes saved rax to `gx_res_after`, restores rax/rdx, and jumps to the original return address. Thus creation/Map accounting is at intercepted return, while destructor handlers unregister at entry before the displaced destructor prologue resumes. This is source adapter behavior, not independent verification of the game's argument meanings. [guest_abi.h:1–16][abi]; [thunk.cpp:35–132][thunk]; [gx_resources.cpp:440–538,613–695][hooks].

Hook installation is individually fallible: disabled registry returns before setting its thunk; mismatched prologues are refused, as are stub allocation/unprotect failures. A total hook count can coexist with missed paths. [gx_resources.cpp:699–765][install]; [graphics_patch.cpp:1019–1046][patch].

## Identities and producers

| Value | Producer, width and basis | Actual selected consumer; trust limit |
| --- | --- | --- |
| Holder key | 64-bit object address; 1D registration uses high-bit `kMemoryKey \| memory`, with a synthetic holder base `out - 0x18` | `g_by_holder`; an indexing key, not a retained guest reference |
| Memory/range | 64-bit read at holder +0x20; 32-bit bytes at +0x2c | `g_by_memory`, lookup and retirement; guest VA, no physical-alias identity |
| Resource `id` | 32-bit read at +0x28 masked to low 24 bits | Returned/logged by registry and upload census; the selected ahead job and Surface do not carry it as a generation discriminator |
| Host-assigned object `id` | Separate 32-bit `g_obj_next.fetch_add`, starting at 1; shader/layout/view/sampler object addresses | SRV ID is captured in `obj_tex_id` and passed to `texture_view_by_id`; distinct from resource `id` and from `VkImage`/`VkImageView` handles |
| `write_seq` | 64-bit global atomic starts at 1; creation with nonzero initial-data pointer gets increment+1, otherwise 0; found-holder Map gets increment+1 | `census_upload` compares against Surface `gx_seq` to attribute an already selected upload; not a byte hash or fence |
| `created_flip` | 64-bit snapshot of `hle_video_flip_count()` at registration | Strict `>` newer-overlap query; video flip completion count, not per-resource generation or submission serial |
| CP submitted/retired totals | 64-bit aggregates: async queue insertion / completion of CP job body | Retirement entry `after` threshold; software job counts across queues, not a GPU fence or job-identity prefix |
| Host submission/completion | Slot `serial = g.flushes`, then `flushes++`; submitted serial+1 published after queue-submit attempt; completed serial+1 updated on successful slot retirement | Recorder/submit wait and deferred-object cleanup; submission attempt and fence completion remain separate |

The resource field reads, same-holder and exact-same-base replacement are in [gx_resources.cpp:252–299][register]. The 1D adapter and descriptor capture are in [613–683][hooks]. Object IDs use a 2^17-slot table with at most 64 probes; full-table insertion increments its own failure counter. That capacity limit belongs to the object table, not the dynamically stored holder registry. [163–209][objects]. SRV ID capture and optional word-at-creation comparison: [gx_trace.cpp:974–997,1656–1662][gxtrace]; actual renderer selection: [render.cpp:8558–8576][render]; ID memo: [textures.cpp:2743–2788][idmemo]. The diagnostic word check is off unless requested, so source immutability assumptions must not become proven invariants.

A readable resource field whose masked low 24 bits are **zero** is not rejected by `register_holder`; zero original resource ID does not itself prevent registration or eligible ahead queueing. [252–299][register]. Separately, host object lookup returns zero for null or missing objects; an unseen object or failed bounded insertion can therefore supply no host ID. Same-address object re-registration finds its existing slot and replaces its ID with the next counter value, rather than treating that address as a missing object. Counter wrap remains unqualified. [184–209][objects], [797–823][objectlookup]. For a resolved renderer image, nonzero selected host ID chooses `texture_view_by_id`; zero chooses `texture_view` using descriptor words. When enabled, `check_object_words` also returns zero on a checked word-hash mismatch and thus selects that fallback. This is a positive fallback path, not universal successful texture resolution or proof of ID/descriptor immutability. [gx_trace.cpp:974–997][wordcheck]; [render.cpp:8558–8578][render].

Flip basis: `finish_flip_locked` increments a port's count; completion paths store it in `g_flips_done`; the getter loads that atomic. Multiple registrations within one flip have equal `created_flip`. [video.cpp:148–155][video], [465–470][flipstore], [903][flipget], [1113–1116][flipdirect]. Counter wrap, unseen creators and original game-ID uniqueness are unqualified. Host completion/slot fields are declared separately in [gpu_internal.h:210–215,291–313][slotfields].

## Creation, Map and lookup

Registration requires successful safe reads of the listed fields; an unreadable field returns without adding a **new** entry, before replacing an old same-key record. On successful reads, a same-holder replacement erases the previous index, and exact base reuse removes the earlier holder record before assigning the memory key. This is not a scan or proof of nonoverlapping physical allocations. [252–299][register].

`gx_res_after` counts nonzero low-32-bit return values for the three holder creators, but that error branch does **not** return early: subsequent registration still depends on output/field reads. The 1D creator uses a type check on its output struct instead. An error counter alone cannot prove no entry was registered. [gx_resources.cpp:613–683][hooks].

The later caller phase matters even when those field reads fail. `register_holder` supplies no success result to `gx_res_after`, which still searches `g_by_holder` for the selected key, can update a found type-2/3 record's T# from the captured thread-local descriptor, copies the record and calls `create_ahead`. For a non-1D output that yields a nonzero holder key with **no retained entry**, failed reads leave the later search absent and no ahead call follows. With an old entry **retained at that same key**, failed reads leave it available to that search; enabled ahead, eligible old type/initial-data/memory, valid captured T# and queue capacity can permit queueing from that old record. This is no newly installed record, not necessarily no queued work. The 1D path additionally recomputes its memory-derived key; the non-1D conditional is not generalized to every 1D failure. Original producer error/output behavior and the natural interleaving remain UNKNOWN; no reachable stale upload is demonstrated. [gx_resources.cpp:649–683][caller], [340–367][ahead].

For a non-ring Map, `note_map` is called regardless of result. It rereads the memory field before taking `g_mu`, then increments a found entry's sequence even for an unchanged pointer, an unsuccessful memory reread or a non-write Map type. A changed nonzero pointer reindexes the entry; an unseen holder only increments `g_map_unknown`. It neither compares bytes nor waits for subsequent caller writes. [419–438][map]; [623–625][hooks].

`gx_resource_at` takes `g_mu`, selects the greatest indexed base at or below the query VA and checks the requested end against that record's end; it optionally copies `GxResourceInfo`. The mutex ends with the call. It does not increase a guest reference count, retain ownership or transfer a lifetime token, and does not explicitly test `alive`. Its arithmetic has no explicit overflow rejection; using a normal bounded range is a premise, not a universal integer-range guarantee. `newer_overlapping` additionally tests `alive` and a strictly later flip, but relies on the comment's nonoverlap assumption for its predecessor search. [882–913][lookup]. A Map move into an occupied base simply assigns the memory index; it does not run registration's old-holder removal or set `alive` true. Thus a retained, memory-release-invalidated holder later mapped to a different nonzero pointer can be indexed with `alive=false`; lookup success alone cannot override that raw field. These are conditional source deductions, not observed resurrection/alias bugs. [419–438][map], [859–880][memrelease].

## Queued creation and the real texture consumer

Only enabled, initially populated, nonzero-memory resources of types 2/3 with a captured thread-local T# enter `create_ahead`. It saves eight descriptor words, fills their base address fields, and saves memory and byte count. No holder key, resource ID, write sequence or flip is saved in `AheadJob`. Queue capacity is 4096; absent T# or full queue declines ahead work. The worker pops a job, checks current range coverage, then calls the host adapter. The range check and host call do not hold one common registry lock. [gx_resources.cpp:308–367][ahead].

`host_gpu_texture_create_ahead` takes `g.mu`, requires `g.ok`, and calls `textures_create_ahead_locked`. The consumer decodes the base (with a mapped low-address fallback), refuses **any existing Surface at that base**, can defer ahead creation for VRAM reserve, and otherwise resolves the saved T# through `texture_view_uncached`. It returns true only when a non-null view and nonfailed surface exist. True is not CPU prep completion or GPU execution. [gpu.cpp:6688–6695][adapter]; [textures.cpp:55–69][base]; [2913–2936][aheadconsumer].

The resolver first considers existing render-target aliases, including a limited current-registry T# dimension check for a larger texture reusing a target's address. A successful alias can return without making an ahead Surface. It then validates descriptor type/format/extent, constructs mip layout and checks mapped source coverage before a new Surface. The ordinary bind path replaces a cached Surface on differences in format, width, height, type, layers, or insufficient mip count; it defers the old image/views rather than destroying immediately. These are real safeguards and must be included when considering a saved A job after B takes the range. They are not comparisons with A's saved resource identity. [textures.cpp:2233–2553][resolve].

If a Surface is already present when the old job arrives, ahead creation is refused. If the old job arrives first after range reuse and no Surface exists, the inspected consumer can resolve its saved descriptor against currently mapped memory; the next bind can replace an incompatible image or refresh compatible content. Whether this interleaving is game-reachable, harmless or faulty remains UNKNOWN. Same dimensions alone do not prove equal tiling, byte content or lifetime. The selected path has no original-resource token comparison; that narrow absence does not exclude synchronization elsewhere.

Refresh is driven by write-watch dirty pages and scheduled sampled/whole-content comparisons, with guards for mapping, prep readiness, `gpu_written`/`cp_dirty`, and once-per-recording/backoff policies. `census_upload` records `write_seq` when an upload is selected; it does not itself trigger the upload. Watched registered CPU surfaces usually skip hashes with a one-in-64 check, conditional on flags; exact hashing is size/budget limited. Memo hits retain refresh; descriptor-word memos verify words and flags, while ID memos check object ID, epoch and flags. This is a set of scoped refresh policies, not complete alias/write coverage. [textures.cpp:1623–1872][refresh]; [2672–2788][memo].

## Upload preparation is another lifetime boundary

`upload_surface` checks mapping and arms a watch before reading, then puts a raw guest `src` pointer and layout into `TexturePrep`. CPU preparation untiles from that pointer and then hashes memory; no source-byte copy or guest lease is carried by `TexturePrep`. CPU async jobs are retained in `g_batch_preps`; the pre-submit path waits for them before GPU copies use staging. A waiter can run an untaken job itself. The GPU untile route instead records imported-source/scratch work and queues a hash-only prep that is **not** in `g_batch_preps`; `settle_prep` waits before consuming its hashes. Consequently a wait for CPU upload staging does not establish completion of every hash-only guest read. [textures.cpp:823–940,968–976][prep]; [1051–1239][upload]; [3344–3351,3518–3525][prewait].

These ownership mechanisms retain the prep object and staging work, but the inspected path does not demonstrate retaining the guest allocation until all reads finish. Mapping checks in `hle_kernel_va_mapped` return a thread-local snapshot answer; watch arming takes the map lock for checking/protection and releases it on return. Unmap cuts mapping records, forgets watches, notifies GX and then performs host unmap outside the map lock. None of those inspected helpers transfers an enduring source lease. An external game allocator/job barrier could supply the missing ordering; its applicability to detached ahead/prep workers was not established. [kernel.cpp:327–440,476–500,719–800][kernel]. No reachable use-after-free is claimed.

## Registry retirement, host retirement and fence completion

Texture destructor entry removes holder/index records under `g_mu`, then outside it calls `retire_memory` for an alive nonbuffer entry. Buffers only release whole watch pages. Memory-release notification invalidates entries **whose bases start inside** its range, erases those indexes and queues retirement of the supplied range (32-bit clamped length), except when the memory index is empty. A resource starting before a partial unmap is not visited by that loop. `memory_protected` is a counting notification; in this kernel path protection changes also go through `maps_cut_locked`, which already issued release notification before pieces are re-added. Do not infer protection leaves registry membership unchanged from the notification's name. [gx_resources.cpp:380–415,837–880][removal]; [kernel.cpp:407–470][kernel].

`release_pages` rounds inward to whole 4 KiB pages and calls `write_watch_release` before queuing the host retirement with the current submitted CP total. Watch release makes tracked pages writable and stamps them changed; this is not measured byte mutation. Forgotten watch pages also read dirty. Registry membership, page protection, retirement queueing and object destruction therefore diverge. [gx_resources.cpp:380–389][removal]; [write_watch.cpp:231–250,445–481,489–506][watch].

The adapter queues `{base,bytes,after_submitted}` under a separate retirement mutex, without waiting for the GPU lock. At `textures_before_submit`, due entries satisfy `after <= hle_gnm_retired_total()`. Only surfaces whose bases start inside the retirement range are visited. Each is kept if a **current** GX range covers its full source span; otherwise views/images are deferred on the current recording slot and the Surface is erased. This prevents indiscriminately destroying a currently registered replacement. It does not require it to be the original resource. [textures.cpp:3295–3351][retirement]; [gpu.cpp:6693–6695][adapter].

The submitted total increments per async job enqueued; retired total increments after CP walking, a conditional `host_gpu_submit`, and the job callback. Totals aggregate per-queue jobs; synchronous queue-0 mode instead walks and flushes directly without these increments. A retired total reaching a snapshot is not itself proof that every particular earlier job from every queue retired: that requires ordering/reachability premises beyond an aggregate count. It certainly is not GPU completion. [gnm_exec.cpp:2120–2130,2197–2297,2367–2432,2502–2503][cp].

Host submission separately assigns the slot serial, waits for batch prep, and routes recording to recorder/submit thread or `vkQueueSubmit`. [gpu.cpp:5170–5268][gpu]. Recorder replay ends the command buffer and forwards a submit job; submission publication means the queue-submit attempt returned, including its error path. [recorder.cpp:398–409][recorder]; [gpu.cpp:144–200][submitthread], [531–550][subadapter]. Slot retirement waits for this handoff, then `vkWaitForFences`. Only successful fence wait runs normal destruction of deferred views/images/memory/ranges and advances `completed_submits`. Timeout/device-lost wait keeps held objects and stops further GPU submission; submit failure has a separate idle/return branch. Neither an error flag nor CP retirement is relabelled successful GPU completion. [gpu.cpp:3943–3983][fence], [4165–4247][slotretire], [4655–4663][deferimage], [4904–4917][deferview]; [recorder.cpp:812–835][subwait].

This supports the implemented normal fence-delayed destruction policy for the inspected Vulkan queue and slots. It does not establish safe guest VA reuse, all external users, missed registry hooks, or every failure/shutdown path.

## Source-faithful positive and contradictory cases

These are branch checks against source, **not executed fixtures or game traces**. Their premises are raw fields/order, not checker-generated flags.

| Case and applicable phase | Inspected outcome | Contradiction or remaining premise |
| --- | --- | --- |
| Readable holder with no existing key, nonzero initial-data pointer, captured T#, types 2/3 | Registration gets sequence; eligible ahead job queues | Failed field read at an absent key, no T#, disabled ahead or capacity prevents this path; pointer presence does not prove copy completion |
| All resource field reads succeed, masked resource ID is zero; other eligibility holds | Resource record can register and eligible ahead work can queue | Zero original resource ID is not the host-object missing-ID test; original uniqueness is unqualified |
| Resolved renderer image, selected host object ID nonzero versus zero | Nonzero selects ID memo; zero selects descriptor-word resolution, including enabled checked-word mismatch | Unseen/failed insertion can yield zero; same-address re-registration updates slot ID; neither branch guarantees a non-null view |
| Non-1D output yields nonzero absent key; one registration field read fails | No new record; caller search remains absent, no ahead call | Requires absent-key premise, not just the failed-read flag |
| Non-1D output yields retained same-key record; one registration field read fails | Old record survives; caller may update its T#, copy it and queue eligible ahead work | Requires eligible old fields, captured T#, enabled ahead and capacity; producer/error schedule remains unknown |
| Known holder at Map return, unchanged pointer, no subsequent byte write | Sequence still advances | Disproves sequence-as-byte-change inference; result/type does not gate increment |
| Unknown holder at Map return | Unknown counter, no new entry/sequence | Observation gap is not proof no writer exists |
| Range covered now; then A removed or moved | Lookup can succeed before removal and fail afterward | Earlier success supplied no lease; alive/range/arithmetic assumptions need inspection |
| Old A job, B at same range; B already has a Surface | Ahead consumer refuses existing base | Falsifies a claim that every old job overwrites B |
| Old A job, B covers range, no Surface; supported saved T# and mapped computed extent | Current range guard can pass; consumer may make Surface from A descriptor/current memory | No original ID check; next bind replacement/refresh and actual schedule determine consequence; no bug demonstrated |
| Compatible descriptor; `!g_refresh_once` or `sf.refreshed_serial != g.record_serial + 1`; `watched && !gpu_written`; watch detects dirty pages | Watch branch calls census and `upload_surface`; census can attribute an advanced sequence | Same-recording guard can return before this branch; `gpu_written` bypasses it; neither the call nor a differing sequence establishes upload success |
| CPU async prep queued | Batch wait completes untile before submitting staging copy | Hash-only GPU-route prep is excluded from batch wait; no guest lifetime is obtained by staging readiness |
| Retirement threshold due, B still covers surface span | Surface kept | Falsifies immediate-destroy-on-unregister inference |
| Due, no coverage | Surface erased; objects placed on current slot dead lists | Before slot fence succeeds, deferred objects remain; CP threshold alone is insufficient |
| Fence timeout or loss | Normal destroy/completion branch is skipped | Cannot call held memory reusable on timeout; separate submit-failure/shutdown paths remain qualified |

## One next question, branches and stop rule

**Question:** What producer-side ordering, if any, keeps the allocation identified by `TexturePrep::src/base/total_src` valid and authoritative from `upload_surface` queueing through `run_prep`'s last guest read, including GPU-route hash-only jobs?

The smallest discriminator is an attributable ordering at this exact boundary: allocation identity/range and saved descriptor at prep enqueue; last raw guest read/prep completion; intervening holder removal, range re-registration or `host_unmap`; and the actual barrier/lease if one prevents the overlap. It must distinguish CPU batch prep, hash-only prep and GPU source reads. A mapped-address boolean, increased Map sequence, shared prep pointer or successful staging wait cannot substitute for allocation identity/order.

First inspect the applicable allocator/job synchronization source where publicly available. **Positive branch:** a demonstrated barrier retains that same allocation through every selected read; narrow the contract to that producer/route. **Falsifying branch:** an authorized owned-data interleaving changes/unmaps storage before a selected read with no applicable barrier, falsifying that proposed ownership contract only. **UNKNOWN branch:** the game producer/barrier is unavailable or the schedule cannot be tied to it; retain UNKNOWN and report the exact missing ordering. No experiment is authorized by this dossier. Stop after resolving this premise or identifying the missing public producer; do not infer a game bug, add a broad tracer, or run game/native code to fill it silently.

## Evidence and candidate check record

Author inspected the complete GX registry/header plus the named downstream function bodies and relevant call sites at the pin. The broader files were not audited in full; renderer target internals, all allocator synchronization, shader logic, imported mapping reclamation and shutdown remain outside this bounded result. Comments containing soaks, performance numbers, game Map semantics or hardware claims were not promoted. Reuse is **KNOWLEDGE_REFERENCE**, under upstream's declared GPL-3.0-or-later; no implementation is imported and no license compatibility decision is made.

The source identities below were obtained from Git's pinned tree; they bind bytes, not truth. At the r1 freeze independent review/fresh-reader acceptance were pending. The review, repair and acceptance history is distinguished below. Each candidate is preserved by its linked commit/tag. Author/review/repair/integration token usage and whole-turn elapsed time remain unmeasured/unknown.

Candidate r1 static checks: 24 repository text files decode as UTF-8 without BOM, NUL or carriage return; 108 relative links including 9 local anchors resolve; 94 pinned bbhost citation occurrences (79 distinct URLs) have existing paths and valid line extents at the exact fetched commit; 17 listed blob identities match that commit's Git tree. This is source-location validation, not a new HTTP reachability survey or proof of claims. The Director draft and both earlier review files remain byte-identical to Commons `22445011206afa47772461cf4ad35a9cdf8ebc48`, and RC-0001 retains that entire prior byte prefix. A bounded private-path/token-prefix scan returned zero hits; manual review found only original prose and public-source references. YAML was checked for indentation/list shape and the 17 named source paths against the blob table; no YAML parser was installed. Git whitespace check passed. Eleven conditional source cases in frozen r1 were reasoned through, with zero fixture/game tests; checker counts are not runtime evidence.

Resource closure: only public-source read/fetch and local document/Git work were used. The scratch source checkout remains at the exact detached pin and is outside the Commons tree; no source was imported, no upstream script was executed, no runtime process or mutable target resource was started, and no external write/outreach occurred. The sole Commons writer freezes the local commit/tag before returning it to the parent for review. No background tool handles require resuming.

### Candidate r2 repair record

The frozen independent review of r1, `BRC-GX-LIFECYCLE-01-REVIEW-r1.md`, SHA-256 `f1081dc0468b49b5c80e29d5688fb9ba633cde685007d934541c156cb93de574`, supported RC-0004/0005/0006 and requested two medium documentation repairs. F1 adds explicit zero original resource ID, zero/missing host object ID, same-address re-registration, optional word-check mismatch and actual descriptor fallback distinctions. F2 separates failed-read outcomes for absent versus retained holder keys through the caller's subsequent lookup/dispatch. Four conditional source cases were added and the original fresh-key control was narrowed. The introduction's retirement safeguard is clarified as current-range coverage, consistent with the body's explicit absence of an `alive` test. Only this dossier changed in r2; claim bodies, source inventory, frontier, r1 tag, Director draft and historical review bytes remained unchanged. These are source deductions, not new runtime evidence or upstream bug findings. At the r2 freeze the same-reviewer affected recheck and the separate fresh-reader exercise were pending; the r3 integration below records the completed recheck. Author repair usage/time are unmeasured; unchanged receipts are reused where their inputs did not change.

Refreshed r2 checks: 24 text files, 108 relative links including 9 anchors, and the bounded public-path/token-prefix scan pass with zero reported errors/hits. There are 97 pinned citation occurrences and 82 distinct source URLs; the four changed source locations were checked for pin/path/line validity, while unchanged locations and the identical 17-row source identity inventory reuse r1 receipts. Fifteen conditional source cases are recorded, with zero fixture/game tests. Git whitespace check passes. Frozen review SHA-256 and r1 tag identity were rechecked; every repository path except this dossier is byte-unchanged from r1. YAML/source registry and resource closure are unchanged. No HTTP resurvey, upstream script execution, external write or runtime work occurred.

### Candidate r3 integration and scoped clarification

The parent accepted frozen r2 `9f67163b468ffdc71ada998acb2b0843c0160f68`, tree `458d5e8f2a71f41ea450c56ce643a2c7609e10dd`, dossier blob `37c202a05743099b9db76a6538180e800f336d18`, after the same reviewer's affected recheck. F1/F2 are repaired and accepted at source/documentation scope. R3 copied both frozen reviews verbatim and added links/status records. The parent additionally identified an underspecified positive refresh-case row: r3 qualified it with once-per-recording eligibility, `watched && !gpu_written`, and detected dirty pages, matching [textures.cpp:1712–1750][refresh]. At r3 freeze its focused recheck was pending; the completed recheck and acceptance are recorded below. Fifteen cases remain; all other technical bodies, upstream pins, negatives and the TexturePrep ordering question are unchanged. Report SHA-256 values: r1 `f1081dc0468b49b5c80e29d5688fb9ba633cde685007d934541c156cb93de574`; r2 `060a1633f25ed3ba4e9abac4c0e5475376375a991915e90916631ccfb4babfc9`. Their pending-status statements describe original review time; this integration does not edit that history. Fresh-reader validation and public PR delivery remained pending at this freeze.

Focused r3 checks: eight added/changed text files passed UTF-8/no BOM/NUL/CR, Git whitespace and bounded private-path/token-prefix checks with zero reported errors/hits. Twelve added relative-link occurrences resolved; the unchanged 108-link/9-anchor receipt was reused, giving 120 relative links and 9 anchors across 26 repository text files. Both copied reports matched their frozen original bytes and SHA-256 values. Claim technical bodies and frontier question/body remained byte-identical to r2; RC-0001 retained its entire prior byte prefix; only the named refresh-case row changed within the dossier's technical sections. The unchanged 17-row upstream blob inventory and source-location receipts were reused. No source fetch/hash inventory, HTTP resurvey, fixture/game test or external write occurred. The local r3 pin was frozen for the focused recheck before acceptance.

### Candidate r4 mechanical integration

The parent accepted r3 `54695ff00e3452d94df939b2c86021088e3897d4`, tree `c61a63284e574daa33c5e1270dc7362cbafcabb1`, dossier blob `1aa7a9d21c35bf7ad9b7296ab88abd8439437080`, after the [same reviewer's narrow recheck](../docs/reviews/BRC-GX-LIFECYCLE-01-REVIEW-r3.md) found no outstanding finding. R4 integrated that report verbatim, SHA-256 `956b566013393af87059fca8f27ed36ff19f4fd92f66903624315dacb0ee40c6`, and updated review links/status only. All technical bodies, the qualified fifteen-case table, pins, negatives, older reports, Director draft and RC-0001's prior byte prefix were preserved. R1/r2 evidence was reused at its existing scope; no extra review ladder or target eligibility was implied. Fresh-reader validation was pending at r4 freeze. No external write occurred during author integration; resource closure was unchanged with no live handles.

Focused r4 checks: seven added/changed texts pass encoding, whitespace and bounded public-text scans; seven new relative links resolve, with no new anchors and zero reported errors/hits. Reusing the 120-link/9-anchor receipt gives 127 links/9 anchors across 27 text files. The new report matches its frozen bytes/SHA-256; technical sections and prior record prefixes are unchanged. The 17-row source inventory and source-location receipts are reused, with no upstream fetch/hash or HTTP rebuild. No runtime tests occurred; usage/time remain unknown.

### Candidate r5 final reader integration

The uninvolved reader used only PR #2's public files and linked pinned public source at observed r4 head `273043492d41ac1a42cb3a7c069b31b68b974166`, matching its requested target. Its [frozen answer](../docs/reviews/BRC-GX-LIFECYCLE-01-FRESH-READER-r1.md), SHA-256 `3f74467693778639373f3d861dbf41567eecc51adc260673c3da714fc290f99c`, correctly separated phase/identity observations, downstream safeguards, software retirement, Vulkan fence cleanup and missing guest allocation ordering. The parent accepted this result with no substantive correction. R5 copies the report verbatim and updates status/history only; technical bodies, fifteen cases, source pins, negatives and the TexturePrep ordering question remain unchanged. Earlier pending statements describe their frozen dates. This validates public continuation/readability, not runtime reachability or safe guest allocation reuse. Final public push/PR status and remote verification remain with the parent; the author made no external write. No live handles remain, and no further semantic review is required for this unchanged-content integration.

Focused r5 checks: seven added/changed texts pass encoding, whitespace and bounded public-text scans; seven added relative links resolve, with zero new anchors/errors/hits. Reusing the 127-link/9-anchor receipt gives 134 links/9 anchors across 28 text files. The copied reader report matches its frozen bytes/SHA-256; technical sections and RC-0001's complete prior prefix match r4. Older reports/draft and the unchanged 17-row source inventory are preserved; source-location receipts are reused without fetch/hash/HTTP rebuild. No runtime tests occurred, and usage/time remain unknown.

| Inspected source file | Git blob SHA-1 |
| --- | --- |
| src/engine/gx_resources.cpp | aca314bb5dd768ea24076279a0d25e821d201365 |
| src/engine/gx_resources.h | f6edcb582e141aabfa30384e381fb79f10e9653c |
| src/engine/addr.h | e6801b27f4607c300d9de48823e6d1860eba00c7 |
| src/engine/graphics_patch.cpp | a8f540c6ac2063236469a7e189f65400207ae61f |
| src/guest_abi.h | 0edccbb88f961e38c9a7461262294faa2ab520f8 |
| src/core/thunk.cpp | 57a1512f92899a29ae35a06bfff5c6e020bd3ca3 |
| src/core/write_watch.cpp | fb6876917ca9cd454dd211db8688fa7a6e896a9a |
| src/hle/runtime.cpp | 06d67882c55955447aab5fa9a1d2283403d04503 |
| src/hle/gx_trace.cpp | c1bf02a6d77a5ec0285320f0a6cc7cc85166ea31 |
| src/hle/kernel.cpp | 8c2e25d7cf980a04ebc61e9f05c2bf6ebfe4c22c |
| src/hle/video.cpp | 4a0ce0427b1c77256c9d727e453889dc8824d85f |
| src/hle/gnm_exec.cpp | ca2c289e6b03f6436dcb7540dc21107ba7cdfb0e |
| src/host/textures.cpp | 54b61d74e06a3c124661b97aa58f092950befbab |
| src/host/gpu.cpp | 0ad2859af2ae5f81ef641018c87c29735a507203 |
| src/host/gpu_internal.h | 31657a3a0a95e852e306296cc7feec0f9ee70a91 |
| src/host/recorder.cpp | 6ae4da44444fdb851fb103c86f0481dcd1a765cf |
| src/host/render.cpp | 516e65d340ec977175e78340a74a49da95cf3497 |

[runtime]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/runtime.cpp#L335-L391
[addr]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/addr.h#L5-L16
[abi]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/guest_abi.h#L1-L16
[thunk]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/thunk.cpp#L35-L132
[hooks]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L440-L695
[install]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L699-L765
[patch]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/graphics_patch.cpp#L1019-L1046
[register]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L252-L299
[objects]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L163-L209
[gxtrace]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gx_trace.cpp#L974-L1662
[render]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/render.cpp#L8558-L8578
[idmemo]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2743-L2788
[video]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/video.cpp#L148-L155
[flipstore]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/video.cpp#L465-L470
[flipget]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/video.cpp#L903
[flipdirect]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/video.cpp#L1113-L1116
[slotfields]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu_internal.h#L210-L313
[map]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L419-L438
[lookup]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L882-L913
[ahead]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L308-L367
[adapter]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L6688-L6695
[base]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L55-L84
[aheadconsumer]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2913-L2936
[resolve]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2233-L2553
[refresh]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1623-L1872
[memo]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L2672-L2788
[prep]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L823-L976
[upload]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1051-L1239
[prewait]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3344-L3525
[kernel]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/kernel.cpp#L327-L800
[removal]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L380-L880
[watch]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/write_watch.cpp#L231-L506
[retirement]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3295-L3351
[cp]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gnm_exec.cpp#L2120-L2503
[gpu]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L5170-L5268
[recorder]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/recorder.cpp#L398-L409
[memrelease]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L859-L880
[submitthread]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L144-L200
[subadapter]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L531-L550
[fence]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L3943-L3983
[slotretire]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L4165-L4247
[deferimage]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L4655-L4663
[deferview]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L4904-L4917
[subwait]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/recorder.cpp#L812-L835
[objectlookup]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L797-L823
[wordcheck]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/hle/gx_trace.cpp#L974-L997
[caller]: https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp#L649-L683
