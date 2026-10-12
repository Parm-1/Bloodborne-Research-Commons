# BRC-PREP-OWNERSHIP-01 fresh-reader report r1

Read scope: public PR #4 and linked public source only. Requested Commons head `f7a046b440834280ef9de32392947f0ebc8cdf2d` was confirmed as the open PR head with `gh pr view` before review. The Commons dossier read was `knowledge/texture-prep-source-lifetime.md`; source references below bind `droogie/bbhost@566184a74f071166299bb656c4af479e5bbe2771`.

## Answer

For the same `TexturePrep`, evidence that its queued hash-only guest reads have ended is either (a) observing `state == 2` after `run_prep` returns, or (b) a completed `PrepPool::wait` on that prep. The raw reader is `run_prep`'s two `content_hash_of(p.base, p.total_src)` calls, the latter exact (`src/host/textures.cpp:847-854`). The worker marks state 2 only after `run_prep` returns (`:919-933`); a waiter can claim state 0, run the prep, then mark state 2, or wait for state 1 to reach 2 (`:890-908`). `settle_prep` uses that wait (`:970-977`).

GPU submission does not establish this hash completion. The GPU hash-only route submits to `PrepPool` and stores the pointer on Surface without adding it to `g_batch_preps` (`:1131-1143`); the pre-submit path waits only `g_batch_preps` (`:3344-3351`, called at `src/host/gpu.cpp:5197`). Erase paths remove the Surface record without settling its prep (`textures.cpp:3323-3338`, `:3396-3407`, `:3440-3454`, `:3490-3504`). Thus, after Surface erase, the source offers a completion condition but no demonstrated externally accessible receipt for that now-detached prep: its queued/worker shared pointer preserves object lifetime, not an API for a caller to query or wait on that particular job. The dossier's phrase “pool state or an actual `wait` proves completion” is technically conditional on retaining/obtaining the same prep identity; it should not read as an available post-erase observation.

## Missing premise and scope

Even confirmed prep completion establishes that this host prep stopped its own hash reads. It does not establish that the original allocation was retained, readable, identity-stable, or free of disallowed writers during the reads. The inspected producer/removal paths do not supply the original texture owner's free/reuse and permitted-writer ordering contract; that remains UNKNOWN. No causal game failure or universal safety conclusion follows.

## Source/navigation findings

- Exact route, raw fields, phase and state evidence are traceable in `src/host/textures.cpp:823-875, 883-940, 968-977, 1101-1151, 3344-3351` at the pinned bbhost commit. Submission gate: `src/host/gpu.cpp:5197-5227`.
- The dossier is navigable through its source link definitions and filenames. One precision gap is the post-erasure observability described above; consider one sentence distinguishing a source-defined completion predicate from a live observer/handle after erase.
- Claims remain SOURCE_INSPECTED; no ABI fidelity, fixture, native, GPU-driver or game evidence was encountered or established here.

## Existing checks and my scope

The public author report says its static/documentation checks covered text encoding, relative links/anchors, pinned source bounds/blob identities, write scope and preservation; its focused receipt reports zero errors for the enumerated checks. I did not independently rerun or promote those checker results to source proof. My own evidence was read-only public PR/head and raw-source inspection. No experiments, code execution against the candidate, runtime changes, children or external writes occurred. Usage and elapsed-time measurements are unavailable; scope is this one public PR/head and the linked source paths above.

## Next decision and closure

One next decision: accept the source conclusion with the narrow clarification that a post-erase completion receipt is not exposed by the inspected interface, and keep original allocation ownership/order UNKNOWN pending a public producer contract. No follow-on probe is justified by this source-only commission. All read commands completed; no persistent process, child or mutable runtime resource remains. This report is frozen at the requested path; any correction requires a linked successor.
