# BRC-PAD-SAMPLING-01 — same-reviewer affected recheck r2

Date: 2026-10-13. Outcome: **F1 resolved; no remaining actionable defect found in the affected source/documentation scope**. This is an independent recheck, not acceptance, integration, publication, merge or runtime authority. The reviewer did not author or substantially design either candidate. Parent source-contract PR-delivery acceptance remains pending; human editorial consolidation/merge remain pending.

## Frozen identity and preservation

Commons branch `research/brc-pad-sampling-01`, repair HEAD `6e1a1128a67282460c81ee40b1e5003f7743f04d`, tree `bba33f9d4ce4846df1a49003c1904f09d98109cd`, tag `brc-pad-sampling-candidate-r2`; independently matched and clean. Predecessor HEAD `639254582f7034ff82ffea03e84e18ff3d693d3a`, tree `f4726126c508b75ca1fdaa91c80cda31d7a87a12`, tag `brc-pad-sampling-candidate-r1` remains unchanged.

Independently matched SHA-256s:

- Author r2: `04e38f7066c190f88695f373fba87c6ad9212a415161bfb95c256791b8d6ab6e`.
- Repaired dossier: `4a2e83d656dee92d98447e2c314d6b7c5d792502761ae0e18ef4e030b305ff66`.
- Preserved author r1: `de46b3b40e5228055c82af3bee1d7e44cef8443d7a0aab6f584d629405fbd5e4`.
- Incorporated review r1, also byte-compared with its immutable original: `902fc2df1d7fad061ab6d49ed0903b2c6831aec0ed74d041161a33d12de4fe57`.

Public bbport source remains `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`, independently matched and clean. Affected current-byte blobs match the unchanged pins: runtime.c `0f8a947a52f384668097055c6dbfe432c79a4de8`; probe.c `75ead5c8ffd6955891e88c9741134c47059fc825`; import_names.inc `55e92852fc94db7445614329c44f38377b24e715`; runtime_pad.c `28e02cbfb878fe2ac8f02e9ebfe83c39abd433cf`.

## Affected contract and interaction recheck

F1 is repaired in `knowledge/pad-sampling.md:39` and P16 at line86. Both now explicitly require `(capabilities & 0x1) != 0`, mask `0x1`, bit index0. The positive gives exact NID `YndgXqQVV7c#A#B` and `is_data=0` at a directly reached resolver; its contrary raw inputs use the same NID/non-data setup with capabilities `0x2` or0, plus a separate `0x1`/data-kind negative. No old ambiguous bit number remains in the current contract; the linked historical note quotes the original finding without reinstating it.

Actual [runtime_resolve:204–211](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L204-L211) tests mask1 before its data branch. For supplied0x1/non-data, the [pad call:249–250 and lookup:263–278](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L249-L278), [exact table entry:261](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/import_names.inc#L261) and [pad exports:757–765](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L757-L765) support the conditional ReadState address selection. Supplied0x2 or0 refuses at the initial test. Supplied0x1/data-kind refuses this NID at the data branch because it is neither permitted data marker. Literal names and absent Read/motion-state table entries retain their selected-route limits; none establishes global unsupported functionality.

The small same-blob bound extension to [probe.c:403–408](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L403-L408) is correct: BBPROBE1 supplies zero; other recognized formats read raw uint64 capabilities, unknown bits outside0x1 fail before runtime_start, and strict_imports supplies zero instead of admitted raw capabilities. The narrow assignment seam [runtime_start:70–72](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L70-L72) assigns flags to the resolver state. Thus the direct0x2 contrary case is a supplied resolver-phase model, not an eligible serialized boot. Admitted raw0x1 with strict mode also cannot establish the positive capability premise. No serialized execution or actual call is inferred.

The unchanged [relocation consumer:528–542](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L528-L542) passes kind2 as data, prefers a nonzero resolved address plus addend, and otherwise uses conditional linked fallback or retains its trap address. The repair preserves those distinct producer/selection/consumer phases. Raw-mask positives and contradictions derive from source, not the author's checker or self-generated expected result. No new test was executed or needed for this wording repair.

## Delta, reuse and limits

The exact r1→r2 delta is three paths: modified dossier, new author r2, and verbatim review r1. All135 other paths of the136-path r1 candidate preserve exact Git blobs and modes. P1–P15 are byte-identical. Both claims/frontier, registry, shared routing/logs, all memory/audio/accepted technical and frozen usability records remain unchanged. Whitespace check passed. The r1 fifteen-source/eight-API inventory and complete cumulative preservation/ancestry/routing review are reused; no broad source/API/integration rerun or parser installation occurred. Author preliminary checker assertion failures remain disclosed in its receipt; final mechanical flags are not semantic evidence.

F1 clarifies the existing mask contract; it changes no authority, source pin, target eligibility, consumer, feature semantics or acceptance. Source/model reasoning remains separate from serialized, native-fixture, physical-controller and game evidence. Actual installed library/compiler/caller eligibility, native ABI, SDL event acquisition/freshness, identity/incarnation/lifetime, concurrent snapshot consistency, physical motion/touch/rumble behavior and original-game correctness remain unqualified as in r1. Seven accepted routes, peer-proposed unmerged memory/audio and both usability NOT MET/Issue9 OPEN remain intact. No fourth topic is selected.

## Resource closure and handoff

Candidate, canonical state and source bytes stayed unchanged. All commands completed; no live process/session handle, runtime/UI/device/input resource, child or writer claim remains. No upstream script/build/runtime execution, source import, controller/game input, install, framework, reader, model shopping, external message/publication or push occurred. The sole new artifact is this scratch successor review; r1 remains immutable. Served-model identity, token/cost usage and elapsed-time telemetry remain unavailable/UNKNOWN; no timed experiment occurred.

Parent may decide bounded source/documentation PR delivery; this review grants no acceptance or publication authority. No further author repair is required for F1. Freeze this report before delivery; later contract/pin/phase changes require a linked successor and affected recheck, not an in-place edit or repeated unchanged review.
