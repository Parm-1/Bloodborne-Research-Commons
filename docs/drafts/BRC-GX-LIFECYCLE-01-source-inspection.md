# BRC-GX-LIFECYCLE-01 — GX identity and lifetime: source-inspection draft

**Status:** Research Director working draft, 2026-10-12. SOURCE_INSPECTED for cited bbhost implementation paths; independent affected review and downstream consumer inspection **pending**. This is not an accepted Commons claim, a game test, an upstream bug report, or a recommendation to import code.

**Question:** Does a resource ID, Map event or successful address lookup establish the byte version a texture consumer sees, or when that resource can safely retire?

**Provisional answer:** No single observation inspected here supplies the complete contract. The code separates registration, guest-address indexing, Map-event accounting, queued texture work and retirement handoff. Downstream consumer and completion code must be inspected before describing end-to-end correctness.

## Source identity

- Commons input: [seed commit fff36c9](https://github.com/Parm-1/Bloodborne-Research-Commons/tree/fff36c9f5145fd0e93c429ae8743758ddf25dd58).
- Existing [RC-0001](../../claims/RC-0001-gx-resources.md) is a header-level claim. It remains independently reviewed **only at the header/documentation scope**; this draft neither rewrites nor promotes it.
- Primary bbhost source: [src/engine/gx_resources.cpp at 566184a](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp), Git blob aca314bb5dd768ea24076279a0d25e821d201365.
- Header: [src/engine/gx_resources.h at 566184a](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h), Git blob f6edcb582e141aabfa30384e381fb79f10e9653c.

The registry implementation was inspected through the complete source body in the Director's research stage. No game binary, native fixture, external code or GPU experiment was executed. Comments about Bloodborne's internal layout and its original ABI are **upstream author reports**, not independently verified game behavior.

## Source path and distinctions

| Phase | Inspected function | Supported statement | Not established |
| --- | --- | --- | --- |
| Hook setup | gx_resources_install | Installs selected prologue hooks, can reject unexpected prologues and supports disabling the registry | Complete natural game-path coverage |
| Creation return | gx_res_after → register_holder | Reads selected holder fields and indexes an Entry by holder and guest memory base | Original producer semantics, all creations, all physical aliases |
| Map return | gx_res_after → note_map | Advances sequence for a found holder; reindexes moved memory | Byte mutation, coherent snapshot or successful consumer uptake |
| Range lookup | gx_resource_at | Under a mutex, looks up covering guest-address memory range and optionally returns a copied record | Enduring caller-held resource lease or GPU completion |
| Ahead job | create_ahead → ahead_thread | Stores descriptor, memory and size; dequeuer checks that a currently indexed resource covers the range | That it is the **same** resource generation, or that downstream fails to revalidate |
| Removal | unregister_holder / gx_resources_memory_released | Removes/invalidates registry entries and initiates separate retirement handling | Completion of every host/GPU user or safe physical reuse |

### GXR-D01 — Multiple identifiers are not a universal generation

The implementation stores a masked 24-bit value read from the game's holder as GxResourceInfo::id. Separately, it maintains a host object ID counter, an event sequence for writes/Maps and a flip counter. Holder keys, memory bases and these counters are different kinds of evidence.

The registration code also handles a reused holder key or reused memory base by changing registry indexes. This does not establish whether all game creators are reached, whether the original ID wraps, or whether physical aliases are co-indexed.

Evidence: [register_holder and counters](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp). **Next question:** which field actually reaches the texture consumer and governs version discrimination?

### GXR-D02 — Map sequence is an event, not a sampled byte value

note_map advances write_seq for a holder found in the registry and, on a changed nonzero memory pointer, updates the memory index. In the inspected gx_res_after Map branch, note_map is not guarded by checking the Map return result. No pre/post content comparison occurs in that path.

A counter can therefore conservatively indicate mapping activity without proving completed mutation. A hypothetical known-holder Map with no subsequent byte change is a useful **reasoning counterexample**, not an executed game trace. A consumer may legitimately invalidate conservatively on a Map; that policy needs to be checked downstream.

Evidence: [note_map / gx_res_after](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp). **Unknown:** how the selected consumer combines this event with dirty ranges, original Map types and actual sampled content.

### GXR-D03 — A successful address lookup is a bounded registry snapshot

gx_resource_at locks the registry, chooses a covering indexed memory base, checks the requested end against the registered extent, and optionally copies the record. When the call returns, its internal mutex is released. The function does not transfer a durable reference to the caller or wait for external users.

The adjacent newer-overlap query compares created_flip strictly against an input threshold. A flip threshold is not, by itself, a complete ordering across every creation, content change or GPU completion.

Evidence: [lookup / overlap queries](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp). **Unknown:** whether the immediate caller obtains longer-lived ownership by some other means.

### GXR-D04 — Registry removal and texture retirement are separate

unregister_holder removes entries while holding g_mu, then performs type-dependent handling outside that mutex. The texture path calls retire_memory, which releases appropriate full pages from write-watch tracking and invokes host_gpu_texture_retire with a range and hle_gnm_submitted_total().

This is an explicit retirement handoff, not evidence that the texture is already released or that all consumers have completed. Buffer handling differs from texture handling.

Evidence: [unregister_holder / retire_memory](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp). **Still to inspect:** implementation of host_gpu_texture_retire, submission-total producer, queue consumption and actual completion condition.

### GXR-D05 — Creation-ahead job identity needs downstream tracing

AheadJob captures a T# descriptor, guest memory address and byte count; create_ahead queues them. When dequeued, ahead_thread calls gx_resource_at for the stored range with no requested record output, and then calls host_gpu_texture_create_ahead with the saved descriptor.

**Locally, the guard tests range presence, not the original holder ID.** This is a research question, **not an accepted stale-resource bug**: the actual lifecycle may exclude address reuse during the window, or downstream creation may recheck descriptor/identity/version.

Conditional examples:

| Hypothetical sequence (NOT executed) | What local guard could see | Missing discriminator |
| --- | --- | --- |
| A remains registered | Coverage present | Is the content/descriptor still A's required version? |
| A is removed and the range is empty | Coverage absent | Exact return and cleanup behavior |
| A is removed, B occupies the same range | Coverage present | Whether B satisfies A's saved job; downstream revalidation or serialized lifetime |

Evidence: [create_ahead / ahead_thread](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.cpp).

## Unfinished downstream work

These files are **leads discovered by path**, not source-body findings in this draft:

- [src/host/gpu.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp)
- [src/host/textures.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp)
- [src/host/gpu_internal.h](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu_internal.h)
- [src/host/recorder.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/recorder.cpp)

Trace actual definitions and callers of host_gpu_texture_create_ahead and host_gpu_texture_retire, together with the relevant submission/retirement progress producers. Identify which data and identity are re-read and what the host guarantees before reuse.

## Independent review requirements

A reviewer not involved in authoring should challenge at least these five distinctions:

1. A Map sequence increment without evidence of changed bytes.
2. A replaced resource at an identical guest virtual range while older ahead work is queued.
3. Removal from a registry versus guest unmap/write-watch changes, queued host retirement and actual GPU completion.
4. Unseen creators, refused prologue hooks, zero/unknown IDs, stale ranges and partial observation.
5. Claims about the game versus claims about how bbhost implements its chosen hooks.

The reviewer must inspect pinned source and downstream definitions, not only this summary. Treat a demonstrated downstream safeguard as a positive correction to the hypothesis, not something to minimize.

## Publication and continuation contract

This file is a **draft for a Codex-reviewed PR**. The next package should contain a concise lifecycle dossier, a small number of atomic source-linked claim records, any justified RC-0001 revision, a narrower frontier, independently checked links and a fresh-context reader answer. Do not copy upstream implementation, run a game, claim memory savings, or promote unreviewed interpretation.

Fresh-reader question: *If a texture's guest address still resolves and its Map sequence advanced, what can be concluded about older queued work and safe retirement? Name the exact inspected code path and one missing premise or falsifier.*

**End state:** Useful source-backed implementation knowledge, qualified at its actual scope, and one specific next experiment or missing consumer fact.
