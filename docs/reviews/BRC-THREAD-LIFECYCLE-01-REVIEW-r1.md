# BRC-THREAD-LIFECYCLE-01 — independent evidence review r1

Date: 2026-10-14. Verdict: **REPAIR REQUIRED — F1**. Recommendation to the parent only; this review grants no acceptance, runtime, publication or merge authority. The reviewer did not author or substantially design the candidate and made no candidate, canonical or upstream changes.

## Exact subject and checked identity

Candidate `43077f06b109322e9338cdd48c819dd2fb3f20f9`, tree `cdc06eaeb35ad73aefe6a1d972908d3786436493`, tag `brc-thread-lifecycle-candidate-r1`, branch `research/brc-thread-lifecycle-01`. Author r1 SHA-256 `7b921f8e9753d0d8514f843ef53d9f12ff5f866678f0ffa850125c0f3f71612b`: both supplied report and repository copy matched. These pins were verified before semantic review. The subject is the new thread dossier, RC-0028/RC-0029, frontier, and five shared routing/registry append deltas.

Integration-only base: reviewed/unmerged file PR21 head `25e747b4f5646578609bb636a9c53c634deba4ed`, tree `a65bd96030be1cf5c460ad8ffa048f439b17d9bc`. Accepted main remained `f293f8b2c2a68a68e221732129d26c86dfc85507`. Sibling review is neither independent corroboration nor acceptance of this topic.

Public source: bbport `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. All seventeen dossier whole-file blobs matched Git objects and current source bytes. Source and candidate checkouts were clean at inspection. Applicable Commons AGENTS, EVIDENCE_POLICY and CONTINUATION were read; public-only scope was preserved.

## F1 — loader admission does not establish typed TCB alignment

Affected candidate locations: `claims/RC-0029-thread-tls-configuration.md:5`, `knowledge/thread-lifecycle.md:41–43` and the defined-positive premises at line73. The conditional general attachment statement omits alignment required by its own C `uint64_t*` TCB accesses. Its alignment discussion identifies requested alignments above64 but does not identify admitted alignments below the typed TCB requirement.

Source-faithful countermodel: a first PT_TLS tuple `(vaddr=256, filesz=1, memsz=1, align=1)`, sufficiently large image, readable one-byte template and otherwise eligible linked setup. Both producer bounds in `scripts/link_modules.py:210–214` / `scripts/link_libc.py:175–179` and loader checks in `src/probe.c:439–441` admit this tuple. The runtime computes offset1, total257 and allocation320 in `src/runtime_thread.c:59,65–67`. Even a successful 64-aligned allocation puts the TCB at block+1. Under an ABI with `_Alignof(uint64_t)=8`, that address is unsuitable for the conversion/stores at lines71–75. The example does not depend on a data race, overflow, failed allocation, unreadable template, invalid loader metadata or an allocator violating its contract.

The C11 committee draft [N1570, section6.3.2.3 paragraph7](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf) makes correct alignment a premise of converting between object-pointer types. The build declares C11; the selected source declares SysV ABI. This countermodel is a source/ABI qualification failure, **not an observed misaligned execution, syscall outcome, crash or compiler behavior**. Successful ARCH_SET_GS is downstream of these accesses and cannot supply the missing C premise. Exact installed type/compiler ABI remains unqualified.

Required repair: state typed TCB alignment as an additional condition for defined attachment/layout positives; distinguish it from requested TLS alignment and fixed base alignment. Preserve an admitted low-alignment raw-field counterexample and avoid describing its undefined C path as a successful positive. Apply the qualification consistently to the atomic claim and dossier premises/limits, with a linked author successor preserving r1. This does not commission an upstream runtime fix, ABI experiment or new framework. Existing align16/64 positives and the align128 countermodel remain useful. Recheck the changed qualification and interactions with cases1/3, zero/default alignment, producer/loader admission, TCB writes and the retained larger-alignment negative; other unchanged source inventories need not be rebuilt.

## Independent semantic coverage

The review inspected actual producers, callers and ordering rather than taking author checks as evidence. Coverage includes the complete selected `runtime_thread.c`; BBPROBE4/5 serialization/rewrite; probe metadata, relocation and native_libc/init/entry gates; runtime ABI/resolver and separate module TLS boundary; key destructor cleanup; decisive low-stack allocator; BbNetHost ABI1 producer and initialization gate; actual NP helper/caller chain; both HLE wrappers and bounded AvPlayer Run/Stop/self-Join edges; selected readable NIDs; and build declarations. Brief dependency reads of NP normalization and BbNetThreadAttr only resolve these selected caller semantics; no complete NP/media/dynamic-TLS audit is claimed.

All eighteen original reasoning rows were challenged against source, including raw contrary fields and phase applicability:

| Rows | Checked positive and decisive contrary |
|---|---|
| 1 | `(256,8,24,16)` yields offset32/total288/allocation320 and nonoverlapping TCB slots; align0 substitutes16. Readable template and successful actual attach remain separate premises. Its safe numeric example survives F1. |
| 2 | filesz25>memsz24 fails loader admission before setter; signature/capability cannot override it. |
| 3 | memsz65/align64 yields offset128 and preserves64 alignment; a legal64-aligned base congruent64 mod128 defeats requested128 alignment. F1 supplies the missing low-alignment challenge to the general statement. |
| 4 | Exact nine-byte match in executable type1 file-backed span changes only first byte64→65; alternate encoding and embedded data are not instruction-boundary/fidelity proof. |
| 5 | `linked && !strict_imports && (capabilities&1)` gates setters/main attach before initializers; strict mode bypasses that branch. Module-init0, main entry and guest thread entry are distinct phases. |
| 6 | Publish/out precede pthread_create; create0 follows successful host create under API premises, while attach/entry can be pending or already ended. Output alone is not readiness. |
| 7 | Ordinary entry receives supplied argument, stores returned pointer, runs cleanup and writes finished before returning. Finished1 is a pre-termination field. |
| 8 | A current guest-created thread with a live setjmp stores explicit-exit value and longjmps to cleanup/tail; host_owned instead exits21. No unwinder guarantee follows. |
| 9 | Sole ordered eligible matching pthread_join success establishes termination of that host thread; joined1 precedes wait. Wrapper returns stored t->result, ignoring actual host value; bypass/cancellation lacks that result guarantee. |
| 10 | Serial repeat join rejects22, eligible current self rejects11, host_owned rejects3 first. Equal pointers alone do not establish registry membership. |
| 11 | Guest detach writes detached1, ignores pthread_detach result and returns0; host error, unfinished thread and later guest join rejection can coexist. No defined racing detach/join scenario is inferred. |
| 12 | First host attachment records pthread_self/host_owned and publishes after attach; reuse finds current. HLE func return has no guest host_start cleanup/finished tail; guest join/exit reject/stop. |
| 13 | Record remains in registry after matching join and ordered recorded getters can work; this proves neither live host identity nor safe reuse of expired pthread_t. Record/TLS and caller-mapped stack are not freed by lifecycle. |
| 14 | Guest attr16384 is admitted, but create requests327680 after min/margin; ignored setter results and map fallback prevent effective-stack inference. Recorded guard8192 is not enforced guard policy. |
| 15 | Serial core priority/affinity getters return stored fields; no scheduling/affinity host calls enforce them. NP policy/inherit/priority/affinity adapters return0 without forwarding those fields. |
| 16 | Stable key destructor receives a cleared nonnull value; ordinary no-repopulation cleanup reaches an empty round. Repopulation permits residual values after four invocations; unused/no-destructor keys are skipped. Cancellation/fault/reentrant nonreturning behavior is excluded. |
| 17 | Helper stack8192 returns positive22 after temporary attr destruction; core null-out returns encoded22. Host create/join failure stops21 rather than becoming a masked recoverable return. |
| 18 | HLE Join checks joinable and takes self-detach versus external join call; Stop requests token then Join. Request/self-detach does not demonstrate cooperative stop, captured-object lifetime or termination. |

No further actionable defect was found in these original rows within their stated ordered, normal-path scope. F1 affects the broader attachment qualification rather than invalidating the existing align16/64 row arithmetic. Required ordering, live/readable pointers, stable borrowed metadata/attrs/keys and ordinary destructor returns prevent the rows from treating undefined C races as positive observations. These remain source/model cases, not serialized artifacts or fixtures.

## Separate primary API evidence and limits

The reviewer read all six cited primary Linux man-pages descriptions: [create](https://man7.org/linux/man-pages/man3/pthread_create.3.html), [join](https://man7.org/linux/man-pages/man3/pthread_join.3.html), [detach](https://man7.org/linux/man-pages/man3/pthread_detach.3.html), [setstack](https://man7.org/linux/man-pages/man3/pthread_attr_setstack.3.html), [arch_prctl](https://man7.org/linux/man-pages/man2/arch_prctl.2.html) and [aligned_alloc](https://man7.org/linux/man-pages/man3/aligned_alloc.3.html). They support the paraphrased create/start ordering, matching successful join termination, detach without wait, caller-stack/guard responsibility, GS platform/error scope and allocator base alignment. Their mutable man-pages6.19 colophons identify tarball fetch2026-09-09, consistent with the candidate. Exact API bytes are not frozen and do not identify installed libc/kernel/compiler/standard-library artifacts. N1570 was additionally consulted solely for F1's typed-pointer C premise, not runtime proof.

The meaningful supported positive remains: under correct API/ABI, matching host identity and ordered eligibility, successful host join terminates that host thread. Ordinary stored result/key-tail guarantees additionally require the selected return/explicit-exit path; they are not required for the narrower host-termination conclusion. Host-managed release consequences do not retire separately allocated guest record/static TLS/caller stack or transitive work. Shared zero DTV, offsets, GS call and exact byte rewrite do not establish original-game TLS ABI, machine GS state, rewritten-instruction reachability or dynamic TLS lifecycle. Source comments about PS4/FreeBSD/compiler/game behavior stay PROJECT_REPORTED. Runtime, native fixture, serialized, original-game, device, scheduler/hardware and fidelity evidence are absent; absence is a limit, not a demonstrated failure.

## Affected integration and mechanical checks

The ten-path delta stayed within five shared paths and five new topic/report paths. The 150-path base has145 protected paths outside the five shared grants; each retained its exact object and mode, including original file PR21 technical/review/failed-usability records. Four shared append prefixes match baseline; removing only the added source-registry block recovers its baseline bytes. Git whitespace check passed. Accepted main/source pins were unchanged. Existing author source/hash/link checks were treated as mechanical leads; this review independently verified identity/source blobs, actual delta preservation and decisive semantic content, without claiming a new complete link-count or YAML-parser qualification. Candidate preserves both failed usability links and Issue9 OPEN/NOT MET; no new remote Issue9 status query was made by this reviewer.

## Closure and next consumer

F1 was batched directly to the same author and parent; parent owns activation of the idle author. Author owns a versioned in-grant documentation repair, preserves candidate/report r1 and returns final successor pins and delta to this same reviewer. After affected recheck, the parent may consider conditional SOURCE_INSPECTED acceptance; this review does not accept for the owner. No change of authority or architecture is proposed.

Reviewer writes are limited to this report. No descendants, background process, runtime thread/fixture, UI/test desktop, device, source writer, build, upstream scripts, dependency installation, private state/source/data access, reader retry, source import, posting, push, merge or host-register operation occurred. Read commands completed; no owned live handles require resuming. Assigned reviewer is Sol/high; independently served-model telemetry, tokens/cost/usage and measured elapsed scope are UNKNOWN. No additive billing or model-equivalence inference is made. Freeze and final SHA-256 are delivered separately to avoid circular self-identity.
