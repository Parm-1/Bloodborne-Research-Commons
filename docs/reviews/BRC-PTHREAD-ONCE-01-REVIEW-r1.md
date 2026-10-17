# BRC-PTHREAD-ONCE-01 — independent source review r1

2026-10-17. Outcome: **no actionable finding in the reviewed conditional SOURCE_INSPECTED contract**. This is an independent review result for the root consumer, not acceptance, editorial approval, merge authority or runtime qualification. I did not author or substantially design this candidate, propose its implementation, or edit its files. No descendants were activated.

## Exact reviewed identity and authority

Commons repository: `Parm-1/Bloodborne-Research-Commons`.

- Candidate commit `fbfe78bfbf50989a31bc07b252ba40f6d7913f78`, tree `554b6fdcc774eaf853e0851ff9d9e6f03635edd9`, tag `brc-pthread-once-candidate-r1` resolving to that commit.
- Base commit `3f063df7ab4c6878fdc56d0e6cf25a8b86bd2025`, tree `98be2f54b823d4aa89ffc510aae3df5ec82440f9`. Supplied PR39 and PR38..30 are integration ancestry only, not corroboration or inherited review acceptance. I performed no remote PR/status/publication action.
- Public bbport source commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`; read-only partial-promisor checkout at `/tmp/brc-buffer-source-eBMo7q/upstream`. This is a selected version, not a freshness assertion.
- Frozen author report: Commons `docs/reviews/BRC-PTHREAD-ONCE-01-AUTHOR-r1.md` and `/tmp/BRC-PTHREAD-ONCE-01-AUTHOR-r1.md`, identical SHA256 `7e85001683073ce661bc4dfd9b2a9056268acb12492f7789cce8aa7eb968da56`, 10755 bytes, both mode0444.
- Inspected existing checker `/tmp/brc-pthread-once-check-r1.py`, SHA256 `734dd8d3a3ce5237ffb8b6441968d944d3c1a9ad819afc86c34a282347c0f988`, 6952 bytes, mode0444. Its content and limitations were reviewed; I did not run it again.

HEAD/tree/tag/base/report identities were refreshed independently. Commons and source had empty porcelain status. All Git commands used `/usr/bin/git -C` with the exact appropriate repository root; no Commons reference was queried in the source clone and no fetch was requested.

Read Commons AGENTS.md, EVIDENCE_POLICY.md and CONTINUATION.md, the bbpc-contract-work and bbpc-closeout skills, the entire dossier, both claims, frontier, frozen author report, and the five shared insertions against the exact base. Only this new temporary review report is writable under this commission. Root retains conditional source-reference acceptance, integration and any external publication; owner editorial acceptance/merge and runtime authority remain excluded.

## Decisive source and contract checks

The six decisive working files were independently compared byte-for-byte with their pinned Git blobs, in addition to reading their selected bodies:

| Source path | Whole-file Git blob | Review use |
|---|---|---|
| src/runtime_kernel.c | `19909ea6f8f5d17b3f20028a324b70b4c5bcec7f` | ERR macro26; once231–244; cleanup274–285; exports309 and resolver315–319 |
| src/runtime_thread.c | `12acdc26c13ca8411b439f4e67eebb37fb8651b0` | Thread record/current33–54; attachment64–109; host_start220–227; create229–255; join260–270; exit279–285; NIDs337–361 |
| src/runtime.h | `3d8cf3c379642f47043a6fe28741116678a2e414` | SysV attribute13, callback type, signed types and resolver/errno declarations |
| src/runtime.c | `0f8a947a52f384668097055c6dbfe432c79a4de8` | Capability assignment70–72; admission/data split204–211; preceding resolver order; NID lookup263–278 |
| src/import_names.inc | `55e92852fc94db7445614329c44f38377b24e715` | Selected once/exit names and exact NIDs |
| src/probe.c | `75ead5c8ffd6955891e88c9741134c47059fc825` | Relocation binding528–542, distinct from executing a call |

These are [pinned public implementation references](https://github.com/deadinside28/bloodborne_pc/tree/3c57da4198ad62039f63f33bfd205b9916518acf), not installed-artifact or target observations. The source/test/build evidence was text only.

| Check category / applicable phase | Independent assessment and discriminating contrary |
|---|---|
| Producer and raw-field semantics | `thread_once` accepts an int32_t pointer and compatible no-argument SysV callback. It acquire-loads the entire32-bit value. Exact1 returns0; persistent3 and -1 neither complete nor select. This is not the separate guard bit predicate. |
| Admission / errors / errno | Both pointers are checked before any control load. Null routine with C=1 still returns ERR(22), with uint32 raw notation0x80020016 under the intended signed32 return ABI. The POSIX adapter directly maps a nonzero result to22. Neither body explicitly writes guest errno on this null-input path. No prediction for invalid nonnull storage/code, nor general errno preservation across callbacks, is justified or claimed. |
| Selection / callback / publication | Only a load of0 attempts strong CAS0→2 with acq_rel success/acquire failure. A win reaches callback before release-store1. O1/O3 support normal winner sequencing; O4 falsifies treating2 as completed data. Callback normal return is necessary for this ordinary publication path and supplies no semantic-success value from the void callback. |
| Failed-CAS observation coverage | For both failure reading2 and failure reading1, source falls through to sched_yield, then a new loop load. O5 and O6 respect this phase; an acquire failure observing1 is not an immediate return shortcut. Scheduling and the subsequent load remain explicit conditions. |
| Matching reader / data identity | O2's later acquire load must read the winner's release1 on the same live control. Under the stated supported atomic and race-free live-data premises this orders covered prior writes. O7 preloaded1 with x=0, a skipped different routine B, and O20 wrong-control/raw-dump observations defeat numerical-state or return-only inference. No source operation retains/copies/validates the initialized data or establishes retirement. |
| Progress / owner identity | The body has no owner record, abort/reset, timeout, error or takeover branch for2. Active initializer O4 and ownerless persistent2 O8 share one raw value. O11 same-control synchronous recursion prevents the outer normal return; O12 distinct-control nesting can complete. No fairness or universal nontermination measurement is claimed. |
| Lifecycle / nonlocal exit | Created-thread `attach` assigns current=t before the still-live `if (!setjmp(t->exit_jump))` entry call. Exported exit assigns heap-record result then longjmps to that same thread's checkpoint, bypassing once238. Its local t pointer is not changed after setjmp; modifying the pointed-to heap record is not modifying that automatic pointer. Static/live C and no other writer avoid a dead-stack-control counterexample. Returning selected key cleanup and matching join can finish with C still2. They are not once completion. Host-owned/main exit instead exits21. This is a valid conditional source route, not a reproduced guest exit. |
| ABI / atomic support / lifetime | The plain int32_t pointer with GCC builtins does not establish opaque guest pthread_once_t layout, numeric initializer, host compiler output/helper, alignment support, lock freedom, callable target ABI or legal mixed plain accesses. The dossier correctly makes those premises/unknowns. O15/17/18 do not assign deterministic outcomes to undefined conflicting access or expired storage. O16 is explicitly quiescent reset outside the ordinary no-reset protocol, not an accepted recovery design. |
| Import applicability | runtime_resolve tests mask0x1/bit0;0x2 alone fails. Data imports return before the function resolver chain. Existing resolver precedence and NID-to-symbol lookup remain necessary conditions. scePthreadOnce metadata/exports and relocation write establish an available source route, not a caller/control/routine receipt. Windows kernel resolution returns0. |

I read all twenty worked rows O1–O20 against these producer branches and premises. They cover normal-return publication, the winner's own subsequent read, later matching acquire observation, selection-before-data, both losing-CAS phases, exact-state impostors, admission, recursion, persistent abandonment, surviving control, asynchronous work, reset and applicability. They are **unexecuted source/model deductions**, not twenty tests or independent observations. Source-faithful positives and contradictory raw-field negatives exist at the applicable phases; invalid/lifetime cases properly withhold a concrete runtime prediction.

## Primary descriptions and limits

Independently opened all four primary references. Mutable documentation bytes were not frozen, and no installed artifact was inferred.

- GCC documents integral-scalar builtins, strong CAS and failure expected-value update, permitted load/store/failure orders, release/acquire relationships and possible external helpers. Its race-free-model assumption makes the candidate's access premises essential. This supports the conditional source interpretation, not generated-code qualification. [GCC atomic builtin description](https://gcc.gnu.org/onlinedocs/gcc/_005f_005fatomic-Builtins.html).
- N1570 §5.1.2.4p25, §6.2.4, §6.2.8, §6.5p6–7, §6.5.2.2p9 and §7.13 separate race, lifetime, alignment, type/call compatibility and jump restrictions. `!setjmp` in an if condition is a permitted context; restoration requires the same thread and live checkpoint. The changed-local exception does not erase a static control or heap record. GCC extension semantics remain separately assumed. [WG14 C11 draft](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf).
- The comparative Linux once page uses its own once-control type and PTHREAD_ONCE_INIT; it supplies no guest numeric layout or ABI. It does not make this body fully POSIX/FreeBSD compatible. [Linux pthread_once description](https://man7.org/linux/man-pages/man3/pthread_once.3.html).
- The Linux yield description gives no guarantee that a particular initializer runs; SCHED_OTHER use is unspecified and the current thread may continue. Its man-pages6.19/2026-02-08 metadata matches the candidate. [Linux sched_yield description](https://man7.org/linux/man-pages/man2/sched_yield.2.html).

## Checker challenge, bounded negatives and preservation

The existing checker validates identities, allowed paths, old-body recovery, link existence, row presence/counts, source blob/bounds association, registry shape and frozen-report equality. It does not parse the once control flow, validate worked-case semantics, fetch/qualify primary descriptions, prove actual caller absence, produce runtime observations or establish review independence. Its `executed_cases=0` is a declared category, not a runtime accounting oracle. I therefore used source branches and primary descriptions, not checker flags, to assess the claims.

The root-supplied unchanged final inventory receipt is reused:287 base files,292 candidate files,10 changed/new paths,282 protected nonshared object/byte/executable-mode identities,5 whole shared-body recoveries,11 source blobs/bounds,20 unexecuted rows,46 local links,23 reference links and4 primary descriptions. I did not rebuild the full historical inventory or rerun the checker. The author's report expressly distinguishes its291-file pre-report check from root's final292-file receipt. Full YAML parsing remains unavailable/scoped only; no parser was installed and no full parse is claimed.

Independently inspected the entire five-path shared delta: README, START_HERE, CORPUS_CHECKPOINT, SOURCE_REVIEW and projects.yaml contain bounded marked insertions reflecting the same proposed status, source-only limits and integration ancestry. The previous bodies, Issue9 OPEN/NOT MET, frozen failures and guard/thread/key scope are preserved under the reused receipt. No acceptance or source lineage was silently promoted in these insertions.

A fresh bounded exact search for thread_once, posix_once, scePthreadOnce, pthread_once and14bOACANTBo in available src/gpu/tests/scripts/tools `.c/.h/.cpp/.inc/.py/.sh` text returned only definitions/comment/export and metadata. The Python test wrapper and relevant C-test text/search, plus build1–24/73–97, were read without executing them. The C368 “at once” rwlock comment is unrelated. These negatives establish neither complete indirect/generated/private caller absence nor target non-use. Tests and build metadata are not atomic, ABI or guest-call oracles.

## Findings, missing evidence and handoff

Actionable findings: **none within the commissioned source-reference claims**. RC-0062 and RC-0063 retain their conditional wording and meaningful falsifiers. No contract, authority or acceptance change is proposed by this review.

Missing evidence remains deliberately separate from defects: actual caller/final binding, target control initializer/layout/access/reset protocol, initializer/data/readers/lifetime owner, installed atomic/compiler/ABI behavior, scheduler behavior and any runtime/game execution are absent. Their absence prevents stronger applicability or runtime claims; it does not contradict this bounded source study. No generated fixture, serialized result, native fixture, runtime/device/GPU/UI or game observation was produced. GPL v2-or-later/per-file/dependency limits support KNOWLEDGE_REFERENCE only.

Root may consume this report when deciding conditional source-reference acceptance and the final status/publication step for one unmerged PR. The reviewer does not accept for root or owner. If the original author receives an ordinary in-grant repair later, preserve r1 artifacts and return a linked frozen successor with exact delta/pins; this same reviewer can recheck affected contracts/interactions when root activates that task. No unrelated test expansion or lifecycle campaign is requested.

Read limitations: all direct shell reads completed successfully. One combined tool response truncated dossier/author output; each complete file was reread separately before assessment. Some PDF locator queries returned index/adjacent context rather than the intended passage; direct section text subsequently supplied the relevant race/jump/type/lifetime material. PDF screenshot requests yielded reference text through the wrapper and are not visual evidence. The author's wrong guessed paths and Open Group403 are preserved in its frozen report, were not retried here, and supply no semantic evidence. The four successful primary-description reads are the references used above.

Resource closure: no candidate/canonical/source edits, build/import, upstream script/test execution, compiler/assembly/initializer/atomic/pthread/scheduler/syscall oracle, target access, private data, external mutation/contact, new reader/framework or descendant. Every shell tool completed synchronously; no owned process/session/lock or runtime handle remains. Only this newly written report is delivered, frozen mode0444 before READY. Implementation/review/repair/integration token usage, billing cost and measured phase time are UNKNOWN; tool-call durations do not supply aggregate task timing, and no usage ledger or savings inference was created.
