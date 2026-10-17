# Pthread once: initialization, publication and abandoned controls

**2026-10-17 — Proposed/unmerged SOURCE_INSPECTED, BRC-PTHREAD-ONCE-01, Batch04 [Issue #24](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/24). Independent source [review r1](../docs/reviews/BRC-PTHREAD-ONCE-01-REVIEW-r1.md) is complete with no actionable finding at candidate `fbfe78bfbf50989a31bc07b252ba40f6d7913f78`, tree `554b6fdcc774eaf853e0851ff9d9e6f03635edd9`. Root accepts the bounded conditional SOURCE_INSPECTED contract for one unmerged reference/editorial PR only; owner editorial acceptance/merge and runtime qualification remain pending. No candidate repair or affected recheck required. [Final author integration r2](../docs/reviews/BRC-PTHREAD-ONCE-01-AUTHOR-r2.md).** [RC-0062](../claims/RC-0062-pthread-once-publication.md), [RC-0063](../claims/RC-0063-pthread-once-progress.md), [frontier](../frontiers/pthread-once.md), [author r1](../docs/reviews/BRC-PTHREAD-ONCE-01-AUTHOR-r1.md).

Consumer: initialization maintainer deciding what a once call's admission, return or raw control observation establishes about publication, contention and abandonment. **A successful 0→2 exchange selects an initializer; normal callback return followed by release1 publishes completion; a later acquire load reading that publication can order its prior writes.** Neither a raw2 nor a return0 by itself proves the desired data protocol, progress, code/data lifetime or a completed initializer for a particular routine pointer.

## Exact source and scope

Public [bbport](https://github.com/deadinside28/bloodborne_pc), commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. This selected pin is not a freshness claim. The non-Windows C11/pthread source is inspected; tests/build scripts remain text only. Whole-file blobs bind the selected bounds below, not complete dependency audits.

| Public path | Whole-file Git blob | Selected bounds and purpose |
|---|---|---|
| [src/runtime_kernel.c][kernel] | `19909ea6f8f5d17b3f20028a324b70b4c5bcec7f` | 1–26, 230–244, 293–319: platform/error constants, complete once bodies, exports and Windows resolver exclusion |
| [src/runtime_thread.c][thread] | `12acdc26c13ca8411b439f4e67eebb37fb8651b0` | 1–54, 64–109, 220–285, 337–361: current-thread identity, live entry checkpoint, exit and matching join, exit NIDs |
| [src/runtime.h][header] | `3d8cf3c379642f47043a6fe28741116678a2e414` | 1–16, 42–46, 54–58: SysV ABI, errno and lookup interfaces |
| [src/runtime.c][runtime] | `0f8a947a52f384668097055c6dbfe432c79a4de8` | 19, 70–74, 204–278: capability assignment/gate, data rejection, preceding resolvers, NID-to-symbol lookup |
| [src/import_names.inc][names] | `55e92852fc94db7445614329c44f38377b24e715` | 67, 651, 698; complete selected-name/NID search: exit and scePthreadOnce metadata, no selected POSIX once alias entry |
| [src/probe.c][probe] | `75ead5c8ffd6955891e88c9741134c47059fc825` | 528–542: relocation resolution before native fallback; no actual once-call receipt |
| [tests/test_runtime.c][test] | `13bdbc2cf037cb2ee0f25c081e0d1dbad945497d` | 1–34, 368; complete selected-name/NID search of 424 lines: harness and unrelated “at once” comment, no selected once invocation |
| [tests/test_runtime.py][pytest] | `8ac0af47d8c662d79194108ed9f2f965e405462e` | 1–44: complete wrapper text, no focused once test |
| [build.sh][build] | `9b7b7c96a1ef8d7b31d2a9e8d8067bb9f4fcf042` | 1–24, 73–97: compiler/dependency discovery and declared C11/pthread runtime/test build, never executed |
| [README.md][readme] | `b7004d7901749ab08dd296ac4f198c230ca19dda` | 394–404: reused GPL v2-or-later declaration and dependency caveats |
| [LICENSE][license] | `9efa6fbc962836e243e20f7f23db062e2c077d28` | 1–8: reused GPLv2 text receipt |

Disposition **KNOWLEDGE_REFERENCE**. No source is imported. Upstream declares GPL v2-or-later; adaptation needs the target's license/per-file/dependency review. The body uses GCC-style builtins and SysV attributes plus host scheduling and thread facilities; the installed compiler/atomic implementation, ABI, libc, host and target remain unqualified. No assembly, compiler, initializer, scheduler, pthread or syscall oracle was run.

The [static guard dossier](static-guard.md) describes a different implementation with owner information and abort; do not transplant its raw word, bit predicate, recursion failure or failed-CAS behavior here. This once body compares the entire signed32 value with1. The [thread lifecycle](thread-lifecycle.md) and [thread key](thread-key.md) dossiers retain their exact start/exit/join and cleanup endpoints; this study uses those paths only to locate an initializer's abandonment. It does not repeat their full campaigns, cancellation/unwinding or host/process exit investigation.

## Primary descriptions, separately qualified

Read 2026-10-17. Exact mutable documentation bytes are not frozen; descriptions do not establish an installed artifact.

| Primary description | Bounded use |
|---|---|
| [GCC memory-model-aware atomic builtins](https://gcc.gnu.org/onlinedocs/gcc/_005f_005fatomic-Builtins.html), load/store/compare-exchange and memory-order sections | Integral scalar access, atomic operations, strong versus weak comparison, expected-value update on failure and conditional release/acquire ordering. GCC assumes a race-free memory model; target support can use external helpers. This is a compiler-description premise, not proof of generated code, alignment support, lock freedom or a guest caller's access protocol. |
| [WG14 N1570 C11 committee draft](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf), §5.1.2.4p25, §6.2.4, §6.2.8, §6.5p6–7, §6.5.2.2p9, §7.13.1.1/7.13.2.1 | Data races, lifetime/alignment/type-compatible access and calls, and valid nonlocal restoration. A same-thread still-live checkpoint is necessary; changed nonvolatile automatic locals in its containing function need care. These language restrictions accompany, rather than replace, GCC extension semantics. |
| [Linux man-pages pthread_once(3)](https://man7.org/linux/man-pages/man3/pthread_once.3.html), description | Comparative API description requires its own initialized once-control type and describes initialization before return. It supplies no numeric guest initializer, control layout, ABI or complete POSIX/FreeBSD compatibility for this body. |
| [Linux man-pages sched_yield(2)](https://man7.org/linux/man-pages/man2/sched_yield.2.html), man-pages6.19, 2026-02-08, caveats | Yield does not guarantee another particular thread runs; behavior with ordinary nondeterministic scheduling is unspecified. No fairness, latency or eventual-publication theorem follows from this call. |

The Open Group 2024 pthread_once page fetch returned403 and is excluded as evidence. The fetched Linux descriptions are references from their maintainers, not executed host calls.

## Producer, phases and access premises

All positive conclusions require a live, correctly aligned and suitably typed signed32 control, valid readable/writable storage, supported atomic builtin semantics for that location, compatible `void (ABI *)(void)` code, and defined ordered access to control and data. The nonnull check does not validate these. Initial zero must be established before sharing. No conflicting ordinary accesses, reset/reuse while calls remain active, control self-modification by callbacks or hidden publisher is assumed in the ordinary one-initialization contract. An ordinary initialization before publication is different from an unordered ordinary write racing an atomic read. `int32_t *` plus `__atomic` is not proof that a guest's opaque pthread_once_t, compiler fast path or plain loads/stores meet these premises.

| Phase / pinned source | Producing operation and supported observation | Limit |
|---|---|---|
| Admission — [kernel231–232][kernel] | Null control or null routine returns SCE raw `0x80020016` before loading control or invoking code. | Even state1 cannot bypass null-routine rejection. Arbitrary invalid nonnull addresses/code are not checked and have no guaranteed recoverable error. |
| Acquire observation — [kernel233–235][kernel] | Each loop loads all32 bits with acquire. Exact1 returns0 without calling this routine. | Raw3, -1 or any other nonzero value is not treated as completed. State1 can be preloaded or externally written; provenance is essential to infer initialization. |
| Selection — [kernel236][kernel] | Only observed0 attempts strong CAS from0 to2, success order acq_rel and failure order acquire. Winning selects that caller's routine. | Selection is before initialization. A loser can acquire-read current1 into its local expected variable, but does not return there: it yields then reloads at234. No shortcut from the guard body applies. |
| Callback — [kernel237][kernel] | Winning caller synchronously invokes its supplied no-argument routine. Caller-owned writes can occur here. | Code identity, desired contents, write extent, callback normal return and all borrowed lifetimes are separate premises. Different routine pointers sharing one control do not get separate turns. |
| Publication — [kernel238–239][kernel] | Only after ordinary callback return does this path release-store1 and return0. | Release publishes prior covered actions, not unfinished asynchronous work, later mutation, semantic correctness, ownership transfer or indefinite lifetime. Successful initializer return is not a status value from the void callback. |
| Contention/other raw values — [kernel234–242][kernel] | Load2 or other values unequal0/1, or a lost CAS, causes sched_yield then another load. | No owner ID, abort/reset, timeout, failure report or takeover exists. Yield result is ignored and grants no fairness. Persistent2 has no path to0/1 in this invocation. |
| Guest exit — [thread220–227,279–285][thread] | In a properly created guest thread, current names its record and its still-live host_start setjmp surrounds entry. Valid guest exit sets result and longjmps to that checkpoint, then cleanup/tail can run. | If called from this initializer, once's store1 is skipped. Under surviving-control/no-other-writer premises raw2 remains. Main/host-owned exit instead stops21 and supplies no retry. There is no once cleanup in this selected path. |

For a race-free ordinary-data positive: initializer A writes `data.x=7` in live shared storage, returns, then release-stores1 to control C. Caller B's later acquire load of **that same C** reads **that store**, returns0 and subsequently reads x with no later conflicting writer; x=7 is supported conditionally. The winning caller's own subsequent read is ordered by its own execution. Reading an unrelated control, reading C before completion, an unordered plain read or merely observing a raw integer in a dump does not supply this publication relation. Nothing in the once body names, copies, validates, retains or frees `data`.

Raw SCE errors above use uint32 bit-pattern notation under the intended signed32 return ABI. [posix_once at244][kernel] converts any nonzero thread_once result to positive22, else0; it does not call fail_posix, return-1 or explicitly set guest errno. For its null-input error no callback/yield runs, so the body supplies no errno write. A successful callback can itself alter errno; the wrapper supplies no general errno-preservation promise. Other loops do not synthesize22 for invalid raw states.

## Import and caller applicability

[runtime204–278][runtime] requires capability mask **0x1 (bit index0)**; flags0x2 alone fails, flags0x1 passes this first gate. This is necessary, not sufficient for binding. Data imports do not reach the once body. Earlier resolvers retain precedence; kernel lookup maps the exact supplied NID through `import_names` and compares the resulting symbol with exports. [names698][names] maps `14bOACANTBo#p#J` to scePthreadOnce and [kernel309][kernel] exports its body plus a pthread_once adapter. No pthread_once entry appears in the complete selected metadata search; naming the adapter or passing capability admission does not demonstrate a POSIX import binding. Windows kernel resolver returns0. [probe528–542][probe] writes a resolved address for a selected relocation before its native fallback, not a caller execution observation.

Fresh exact selected-name/NID search over available `src`, `gpu`, `tests`, `scripts`, `tools` C/header/C++/inc/Python/shell text found only once definitions/exports and the scePthreadOnce metadata entry. Complete runtime-test C and Python wrapper inspection found no selected once invocation/test. Test C368's “at once” describes rwlock holders and is unrelated. This bounded negative does not exclude indirect/generated/private callers, native fallback or other versions. Import comments about game usage are PROJECT_REPORTED; a recorded actual caller/control/routine/data protocol remains UNKNOWN.

## Conditional worked cases — unexecuted

These are original source/model deductions, not generated fixtures, checker outputs or observed schedules. C denotes the same live control; A/B denote compatible live routines. Data/code/control lifetimes, atomic support and ordered access above apply unless a row explicitly identifies the missing premise. “Persistent” means no other writer changes the location. No iteration or elapsed-time bound is asserted.

| Case | Defined premise / phase | Conditional outcome and discriminating contrary |
|---|---|---|
| O1 | C starts0; A writes live x=7 and returns normally; no other writer. | Winner selects0→2, calls A once, stores1 and returns0. Selecting2 alone would be too early to claim x=7/completion. |
| O2 | O1 completes; later call supplies B and its acquire load reads matching release1. | Returns0, B is not called, subsequent covered read x=7. Return0 does not mean this call's B ran. |
| O3 | A's own caller returns through239, then reads its still-live x with no intervening writer. | Its own sequence covers x=7; it need not pretend to be a cross-thread acquire observer. |
| O4 | A wins and pauses before writing x; contender acquire-loads2. | Contender yields/reloads and cannot return on2. Initializer-selected is not initialized-data-complete. |
| O5 | Two calls load0; A wins; B's CAS fails reading2. A subsequently publishes1; B is scheduled and later loads1. | B invokes no routine and returns0 only at235; conditional progress requires these later events, not yield alone. |
| O6 | B loaded0; A wins and publishes1 before B's strong CAS. B's failed CAS reads1. | Acquire failure does not return from this body; B yields and needs a subsequent loop load1 to return. |
| O7 | C is initialized to1 before sharing, x remains0, A is valid. | Call returns0 without A, x remains0. Exact raw1/return0 alone does not prove initializer provenance or desired x=7. |
| O8 | C is valid persistent2 with no active initializer. | Calls yield/reload; no ownership/takeover/error is inferred from2. Same raw value as O4, different owner history. |
| O9 | C is valid persistent3 (low bit set) or -1. | Neither is1 or0; yields/reloads, no routine/return22. A low-bit completion checker would contradict this body. |
| O10 | Null control with valid A, or live C=1 with null routine. | SCE raw0x80020016 / POSIX22 before control load; no callback and no explicit guest-errno write. State1 does not defeat admission. |
| O11 | A wins C and synchronously calls once(C,B) before A can return; no other writer. | Nested call loads2 and repeatedly yields; outer A cannot reach publication. No owner-recursion detection, abort or nested success follows. |
| O12 | A wins C, calls once(D,B) on a distinct valid D=0; B returns, then A returns. | D can publish1 and return, then C can publish1. Recursion alone is not the failure predicate; same-control dependency matters. |
| O13 | A wins C and does not return (for example waits forever on an independent never-satisfied condition); C survives. | C stays2 and no normal-publication return occurs. At-most-one selection in this epoch supplies no liveness. |
| O14 | A runs inside entry of a created guest thread with valid same-thread live host_start checkpoint, and calls the exported guest thread_exit; C is static/live and not reset. | Exit longjmps past once's release; selected cleanup may return and matching host join may finish while C remains2. Thread termination does not complete once. No foreign/stale jump or automatic object abandoned by that jump is used as C. |
| O15 | A normally returns after merely arranging independent later work; its later writer is not covered by a demonstrated completion/order protocol. | Release1 covers A's prior work only. It proves no descendant completion or race-free later read; no value is predicted for conflicting unordered later accesses. |
| O16 | C=1 from completed A; all calls/readers retire; target explicitly atomically resets C=0 while quiescent, then invokes B. | B can win and run: no generation record enforces once across caller-managed reset. This changed protocol is outside O1–O6's no-reset premise; concurrent reset is not a defined positive here. |
| O17 | C initialized0 before sharing by an ordinary initialization; thereafter all conflicting control operations follow the supported atomic/ordering protocol. | Ordinary initialization itself is not a race. A concurrent unordered plain control load/store would instead violate the premise, with no deterministic outcome asserted. |
| O18 | Caller offers a misaligned/dangling/undersized control, incompatible callback ABI/type, or expired data. | Nonnull admission does not validate it. Defined positive contract is unavailable; do not predict22, a crash or successful publication. |
| O19 | Runtime flags0x2 versus0x1, selected sce NID, non-data request, compatible source/platform; all preceding lookup conditions supplied. | 0x2 fails capability gate;0x1 can reach kernel mapping if not resolved earlier. Gate passage alone does not prove final relocation, call or a POSIX alias. |
| O20 | A publishes C=1 but consumer reads a different control D or observes C only through an unattributed raw dump. | Numerical equality supplies neither the same-object release/acquire edge nor initialized-data ownership; require attributable operation/provenance. |

## Consumer decision and remaining frontier

Use RC-0062 as a conditional reference for normal publication with exact control/store/load identity and covered data accesses. Use RC-0063 to reject a universal progress, recursive recovery, abandonment retry or lifetime guarantee. Do not replace target initialization, add reset/recovery or claim full pthread_once compatibility from this study. The [frontier](../frontiers/pthread-once.md) names the smallest authorized successor and its outcome branches. No serialized/native-fixture/game evidence exists here; Issue #9 remains **OPEN / NOT MET**, with frozen failures and usability history unchanged.

[kernel]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_kernel.c#L230-L244
[thread]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_thread.c#L220-L285
[header]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.h#L1-L16
[runtime]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L204-L278
[names]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/import_names.inc#L698
[probe]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L528-L542
[test]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tests/test_runtime.c#L368
[pytest]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tests/test_runtime.py#L1-L44
[build]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/build.sh#L73-L97
[readme]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/README.md#L394-L404
[license]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/LICENSE#L1-L8
