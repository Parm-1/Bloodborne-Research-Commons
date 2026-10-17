# Static guard ownership, retry and initialization publication

**Status — 2026-10-17:** proposed/unmerged SOURCE_INSPECTED BRC-STATIC-GUARD-01, Batch04 [Issue #24](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/24), one outcome/one PR. Independent review and root acceptance pending; owner editorial acceptance/merge pending. [RC-0050](../claims/RC-0050-static-guard-state.md), [RC-0051](../claims/RC-0051-static-guard-publication.md), [frontier](../frontiers/static-guard.md), [author r1](../docs/reviews/BRC-STATIC-GUARD-01-AUTHOR-r1.md).

Consumer: a runtime maintainer deciding what an acquire result, guard word, abort/retry or release establishes about one static object's initialization. **Keep the same guard and initialized object identity through acquire → caller-owned initializer writes → release/abort → later acquisition or compiler fast path.** The useful source contract is conditional mutual exclusion and release/acquire publication, not a guard snapshot as an initialization receipt.

## Exact source and separate descriptions

Public [deadinside28/bloodborne_pc](https://github.com/deadinside28/bloodborne_pc), supplied commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. Selected Linux x86-64 source, no new upstream currency query. Full blobs identify bytes; selected bounds identify inspected text.

| Pinned path | Selected bounds | Full blob | Role |
|---|---|---|---|
| [src/runtime.c][runtime] | 18–21,70–90,146–174,198–222,259–282 | `0f8a947a52f384668097055c6dbfe432c79a4de8` | guard producer, counters and exact resolver |
| [src/runtime.h][header] | 1–18 | `3d8cf3c379642f47043a6fe28741116678a2e414` | ABI and public declarations |
| [src/import_names.inc][names] | 1–13; complete selected-name/NID search | `55e92852fc94db7445614329c44f38377b24e715` | acquire/release diagnostic names; selected abort absence |
| [src/probe.c][probe] | 528–542 | `75ead5c8ffd6955891e88c9741134c47059fc825` | installs resolved addresses, not a call receipt |
| [gpu/shim/bbgpu.cpp][shim] | 305–321 | `d71cfc41a9e532ff1c0e30ccc9073d24726315d3` | separate prefix fallback boundary |
| [tests/test_runtime.c][test] | 1–20,112–121,395–424 | `13bdbc2cf037cb2ee0f25c081e0d1dbad945497d` | actual public scalar and recursive callers, unexecuted |
| [tests/test_runtime.py][pytest] | 1–44 complete | `8ac0af47d8c662d79194108ed9f2f965e405462e` | subprocess expectations and missing-executable skip, unexecuted |
| [scripts/prepare.py][prepare] | 198–219 | `6d4a88119cd7090f560afcec5035751687cfecdf` | import relocation/name candidates, read only |
| [build.sh][build] | 1–23,73–99 | `9b7b7c96a1ef8d7b31d2a9e8d8067bb9f4fcf042` | C11/pthread/runtime glob and test build declarations, read only |
| [README.md][readme] | 394–402 reused license receipt | `b7004d7901749ab08dd296ac4f198c230ca19dda` | GPL v2-or-later declaration |
| [LICENSE][license] | 1–8 reused receipt | `9efa6fbc962836e243e20f7f23db062e2c077d28` | GPL v2 text |
| [gpu/VENDOR.txt][vendor] | 1–5 reused receipt | `4a8603c7854cfb254ae105f8f21b34d36a6cf102` | dependency/lineage limits |

Four separate primary descriptions read2026-10-17: [Itanium C++ ABI §§2.8,3.3.3](https://itanium-cxx-abi.github.io/cxx-abi/abi.html#once-ctor); [WG14 N1570 C11 draft2011-04-12](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf), §§5.1.2.4,6.2.4,6.2.5p27,6.5,7.17.3/5/7; [GCC x86 sysv_abi](https://gcc.gnu.org/onlinedocs/gcc/x86-Attributes.html); [Linux sched_yield](https://man7.org/linux/man-pages/man2/sched_yield.2.html), man-pages6.19, dated2026-02-08/rendered2026-09-09. Mutable documentation bytes are not frozen. These describe comparative ABI/language/API premises, not installed compiler/atomic layout/lock freedom/scheduler or console qualification.

## Callable route, caller and storage premises

With runtime capability bit0 set and `is_data==0`, [runtime:204–221][runtime] directly compares full strings: `3GPpjQdAMTw#q#q` → acquire, `9rAeANT2tyE#q#q` → release, `2emaaluWzUw#q#q` → abort. This direct route does not need the diagnostic table. The table names acquire/release; no selected abort name/NID occurs there. Table absence therefore does not negate the direct abort resolver. Plain symbols or wrong suffixes are not these direct matches; the surrounding/fallback route is only the bounded [existing import study](import-resolution.md), not a global unreachability proof. [Probe:528–542][probe] installs a resolved address plus addend; it does not demonstrate a call. The [prepare candidate list][prepare] is also not a linked-call receipt.

The wrappers take `uint64_t *`, acquire returns int, release/abort return void; [header:13][header] marks System V ABI. GCC describes that annotation's intended calling convention. [Build:74,82,89–90][build] includes runtime*.c in C11/pthread production and test commands and would run the test executable in its --test branch. No command was executed here and no compiler artifact is identified.

There **is an actual public source caller**: [test:112–121][test] resolves the three addresses, passes an ordinary automatic `uint64_t state=0`, asserts owner1, abort0, retry1, release1 and later acquire0. [Test:404–406][test] calls acquire twice on the same guard for recursion. [Python:1–23][pytest] expects normal return0 and recursive exit21, skipping the class if the executable is absent. These are SOURCE_INSPECTED caller/assertion facts, not OWNED_TESTED results or proof of atomic layout. They neither write/read a separate initialized object nor supply a concurrent guard-publication schedule. The printed phrase guard ABI is an upstream test label. Bounded selected-name search in src/tests/scripts/gpu/shim found these tests, resolver, name table and prepare list; it establishes no actual game/compiler-generated caller/order, actual executed tests or global absence of other routes.

The source casts the caller's pointer to `_Atomic uint64_t *`. For the conditional reasoning below, supply a valid, initialized atomic object with the host's required size, representation, alignment and lifetime, and a qualified adapter permitting these typed accesses. A plain eight-byte region or ordinary uint64 alignment is insufficient by itself. N1570 permits different atomic representation/alignment; a pointer cast does not establish object type/effective-type compatibility. The public test's plain uint64 does not resolve this. No null, mapping, extent, alignment or ownership checks occur. Invalid storage does not have a defined error return here.

Guard storage is distinct from the initialized object's storage and semantic lifetime. Neither is allocated, retained, destroyed or validated by these wrappers. Keep both alive through all users/waiters; do not reset/free/reuse the guard during initialization or observation. Reusing an address or copying bit1 to a different object is not preserving guard/object generation identity. `runtime_start` sets capability/canary state, not a guard-owner/counter reset. Reuse [thread lifecycle](thread-lifecycle.md) and [mutex/condition](mutex-condition.md) only for their existing host-thread/lifetime scope; guard tags are their own mechanism, not pthread handles, guest thread IDs or lock holders.

## Guard transitions and owner identity

Let G be the uint64 state value, C=G&1, O=uint32(G>>32), L=G&0xffffffff and t=this host thread's `guard_owner`. These are numeric bits; mapping them to a low-address byte/+4 dword additionally needs byte-order/representation premises. [Runtime:150–151][runtime] says the dumped libc uses that byte/dword arrangement: this console-internal assertion is **PROJECT_REPORTED**, not established by the public test or by the comparative ABI.

[146–166][runtime]: the static atomic uint32 allocator starts1; the thread-local uint32 tag starts0. Before any completion test, a zero local tag takes the old value of atomic fetch_add1. Each loop starts expected=0, acquire-loads G and returns0 if C is set. Otherwise strong CAS compares the **entire state with zero**, on success writes uint64(t)<<32 with acq_rel ordering and breaks. Failure is an acquire observation that updates expected. If its bit0 is set, return0. Otherwise equal upper32 tag triggers the diagnostic and `exit(21)`; a different tag calls sched_yield then retries. After successful CAS, acquired counter increments and return1 transfers initialization work to the caller. The wrapper never invokes an initializer or validates its object.

Under valid atomic storage, distinct nonzero tags, initially zero G, protocol-obeying callers and no reset/foreign write, a successful CAS makes G nonzero with C=0. Another distinct-tag caller cannot CAS zero while that value remains; it retries rather than initializing. This is the useful exclusivity mechanism. A same-tag reentry before completion exits21 rather than deadlocking by waiting. The text recursive/concurrent in the diagnostic must not be read as rejection of all concurrency: different tags wait. Yield is polling, with no timeout, fairness, cancellation, owner-death recovery or finite completion bound. The Linux API description does not guarantee a different initializer will run; source ignores yield's return. Thread cancellation/termination while holding the guard has no cleanup in these bodies.

The allocator and local tags are finite. Atomic unsigned allocation eventually returns0 after values1..0xffffffff; zero is not skipped. On that invocation t remains0 and zero→zero CAS can succeed, reporting1 without installing exclusion. A different caller can then win the same zero state. A subsequent acquire by the zero-tag thread retries allocation because its local value is still0. Continued allocation reuses earlier nonzero tags, with no live-tag set, recycling check or generation. Equal tags on distinct live threads can be misclassified as recursion; thread exit does not return a tag. Even a first call on an already-complete guard consumes an allocation before returning0. These are finite-width source counterexamples, not a claim that an actual run reached wrap.

## Initializer writes, release, abort and observations

[168–174][runtime]: release unconditionally release-stores the whole G=1, then increments released. It neither checks owner/current state nor executes/validates initialization. Abort release-fetch-ands with0xffffffff: it clears upper32 and **retains all low32**, including bit0. For a canonical owner-held G=t<<32, abort yields0, permitting retry; for arbitrary nonzero even L it leaves nonzero even G that zero-CAS cannot acquire. An already-complete1 stays1. Neither operation has a return status or caller/tag validation. They do not undo partial initialized-object writes, unregister a destructor, recover an exception or free the object.

N1570's release/acquire rule supplies a useful conditional positive: if initializer writes W are sequenced before release-store1 on this guard, and a later acquire-load or failed acquire-CAS reads that publication (or applicable release sequence), W precedes the reader's following object accesses under the stated race-free lifetime premises. Merely return1 is before W; observing an arbitrary odd raw value lacks W's provenance. Abort can order partial writes to a later successful acquiring CAS, but does not turn them into successful initialization. Retry still owes correct cleanup/reinitialization and eventual release or abort by its caller.

The [Itanium comparative API](https://itanium-cxx-abi.github.io/cxx-abi/abi.html#once-ctor) describes a 64-bit associated guard, first-addressed byte0 before and1 after construction, other bytes implementation-defined; acquire1 precedes initialization and owes same-guard release/abort. It discusses an optional inline first-byte check and ordering object accesses after an initialization-flag load. It is explicitly not any platform's authoritative ABI. No original console/compiler caller, emitted fast-path load, barriers, exception route or destructor-registration ordering is inspected here. In particular **a caller bypassing acquire on a plain byte read has not thereby executed this wrapper's acquire operation**. Its cross-language/compiled ordering must be established separately. N1570 treats unordered conflicting atomic/non-atomic access as a data race; neither an x86 label nor this C cast qualifies mixed accesses. This is an unresolved adapter/compiler boundary, not a demonstrated target failure.

[18–21,86–90,165,170][runtime]: acquired counts successful CAS paths, including attempts later aborted; released counts calls after the store, even without valid acquisition. Neither counts initialized objects or aborts. Both atomic size_t increments use default sequential consistency, as does tag allocation; publication uses the explicit weaker orders above. Report reads the two counters separately, not one atomic transaction: another reader can see G=1 before released increments. Finite size_t counters wrap; equality does not prove completion or no abort. Recursive exit21 is process termination, not a recoverable guard status; this branch calls host exit directly and does not call runtime_finalize/report first. Host exit behavior is not investigated. Callback registration/finalization and full TLS/exit behavior remain separate questions.

## Conditional source/model cases — zero executed

All rows are original scalar reasoning from the pinned operations, not fixture bytes, compiled code, checker-generated expectations or test successes. Unless a row challenges them, supply valid atomic storage/adapter, stable same guard/object identity, nonzero unique tags, protocol callers and no interfering reset. A and B are distinct host threads with tags7 and9; X is the separate initialized object.

| ID / phase | Positive and contradictory raw fields/order | Supported distinction |
|---|---|---|
| G1 admission | G=0, A CAS writes0x0000000700000000, returns1; X may still be uninitialized | acquired initialization responsibility, not completion |
| G2 waiting | While that G remains, B fails zero-CAS, sees O=7≠9 and yields/retries; A reentry sees O=7=t and exits21 | different-owner wait versus equal-tag termination |
| G3 load completion | A has written X=42 and released G=1; B acquire-load reads that store, returns0 then reads X | conditional publication; changing raw G to3 without W retains return0 but loses initialization provenance |
| G4 CAS completion race | B's initial load sees C=0; A releases1 before B CAS; failed CAS observes expected=1, B returns0 | completion may be acquired at failed CAS, not just initial load |
| G5 bit predicate | G=0x0000000900000001 returns0 even for t=9; G=2 has low byte nonzero but bit0clear and fails zero-CAS | bit0 precedes owner check; nonzero byte/word is not this completion predicate |
| G6 retained even state | G=0x0000000700000002 aborted→2; t=9 keeps failing zero-CAS with O=0≠9 while state unchanged | abort is not universal reset; no finite success claimed |
| G7 canonical retry | A held7<<32, abort→0 after partial X=5; B CAS→9<<32 returns1, then supplies correct X=42 and release1 | retry can initialize successfully; abort alone never completed X |
| G8 abort completed | G=1 aborted→1; later acquire returns0; compare canonical abort→0 | abort retains completion and all low32, does not invariably enable retry |
| G9 unvalidated release | Correct owner release after X writes publishes1; release on G=0 or wrong-owner-held G also writes1 | identical final raw1 lacks proof of valid ownership/initializer sequence |
| G10 owner zero | At allocator old0, t=0, G=0 CAS writes0 and returns1; B can also CAS0→9<<32 | zero-tag wrap violates the nonzero-tag exclusion premise |
| G11 collision | Ordinary A7/B9 waits; after allocator reuse, distinct B7 observing A-held7<<32 exits21 | equal tag is not unbounded unique host-thread identity |
| G12 allocation phase | Fresh t=0 on complete G=1 allocates a tag then returns0; later same-thread calls retain nonzero t | tag count is not count of initializer attempts; zero-tag call allocates again next time |
| G13 publication phase | W before release1 and B acquiring that store orders W; W after release is outside that edge | completion bit and counter cannot repair early publication |
| G14 fast path | B using the qualified acquire observation in G3 has the edge; replacing it with unqualified ordinary byte read supplies no such C acquire receipt | compiler/adapter evidence needed; no deterministic racy outcome predicted |
| G15 identity/lifetime | Same live guard/object keeps G3 meaning; copying1 to another guard/object or freeing/reusing either loses that premise | numeric equality/address reuse does not carry initialization generation |
| G16 statistics | In quiescence one abort/retry/release gives acquired2/released1; snapshot after release store before its increment can still show released0 | attempts versus releases versus completion, not a conservation proof |

The public test provides its own source assertions for canonical abort/retry/release and recursion, separately from these rows. No executed source/model case, serialized sample, native fixture or game observation is supplied.

## Reuse decision and next boundary

**KNOWLEDGE_REFERENCE.** Reuse the state distinctions for one runtime/compiler-adapter review: identify guard/object generation, atomic storage/ABI, owner-tag premises, caller initializer and failure path, publication source and actual fast-path ordering before interpreting completion. Keep the existing wrapper implementation untouched in this research PR. [Frontier](../frontiers/static-guard.md) names the missing premise, outcome branches and stop rule; it grants no execution.

Original prose only; no code/source import. Upstream README declares GPL v2-or-later, LICENSE is GPL v2 text; reused VENDOR/per-file/dependency caveats remain in [registry](../sources/projects.yaml). No license/ABI portability or drop-in reuse approval follows. Actual artifact/caller/order, compiler/atomic layout and lock freedom, installed scheduling, original-console equivalence, native/runtime/game behavior, usability, performance and general deadlock freedom remain UNKNOWN.

Reviewed/unmerged RTC PR #33 over probe-image #32, rwlock #31 and eventqueue #30 is an integration-only predecessor, not corroboration. Prior root conditional reference/editorial acceptance is not owner editorial acceptance. Incorporated main `689e2e29ed67d1c4f5231a1254b93ffd88586bc8` and first five Batch04 incorporations remain unchanged. Issue #9 stays **OPEN / NOT MET**; all failed answers/grades/heads/frozen evidence are preserved. No reader retry or inherited merge/target authority.

[runtime]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c
[header]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.h
[names]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/import_names.inc
[probe]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c
[shim]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/shim/bbgpu.cpp
[test]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tests/test_runtime.c
[pytest]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tests/test_runtime.py
[prepare]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/scripts/prepare.py
[build]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/build.sh
[readme]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/README.md
[license]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/LICENSE
[vendor]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/VENDOR.txt
