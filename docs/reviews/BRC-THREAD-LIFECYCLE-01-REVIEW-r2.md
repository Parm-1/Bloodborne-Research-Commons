# BRC-THREAD-LIFECYCLE-01 — same-reviewer affected recheck r2

Date: 2026-10-14. Verdict: **F1 RESOLVED; no remaining actionable affected source/documentation defect**. Recommendation only: the parent may consider conditional SOURCE_INSPECTED acceptance of the repaired contract and affected integration. This review does not accept for the owner or grant runtime, publication or merge authority. The reviewer remained uninvolved in candidate authorship and performed no candidate/canonical/upstream edits.

## Exact subject and preservation

Repaired candidate `ca5b9b331d6c787faa20c626d8d2cca372c3d20e`, tree `467a2d46921245f47156db619bed57a736a98ba7`, tag `brc-thread-lifecycle-candidate-r2`, branch `research/brc-thread-lifecycle-01`: verified before semantic recheck, checkout clean. Author r2 SHA-256 `385d31b38e90c5611b08e00ad79786d494538acd9d99bf0bea4e608c72017081` matched supplied report and repository copy. Review r1 SHA-256 `e51c05c8750264223832531fa23c2df75f4a885edadac786062024f01cd20e35` matched the original frozen report and newly incorporated verbatim copy. Original candidate/tag r1 remain `43077f06b109322e9338cdd48c819dd2fb3f20f9`; original author r1 bytes remain unchanged.

Integration-only file PR21 base remains `25e747b4f5646578609bb636a9c53c634deba4ed`, tree `a65bd96030be1cf5c460ad8ffa048f439b17d9bc`. Accepted main remains separately owned; the parent supplied its unchanged identity. Sibling file review is not corroboration or acceptance of thread claims.

Public source HEAD/tree still match bbport `3c57da4198ad62039f63f33bfd205b9916518acf` / `ab584d54c478824a75bef51a3f5fe349e5a3c415`, with clean source checkout. The unchanged seventeen-blob source inventory and r1's complete source/caller/API/eighteen-row coverage are reused, not re-audited. No new source acquisition, freshness query, API survey or runtime qualification occurred.

## F1 and changed interactions

The repaired RC-0029 predicate, dossier attach/alignment paragraphs and general defined-positive premises now require actual block+offset alignment suitable for `uint64_t*` conversion and stores before GS setup. They distinguish requested TLS alignment, fixed64 allocator base alignment and typed TCB alignment. Downstream syscall success is no substitute for the earlier C premise. The frontier carries this requirement into any future separately authorized setup observation.

The reviewer re-read only F1's decisive producer/loader/runtime ranges: `scripts/link_modules.py:210–214`, `scripts/link_libc.py:175–179`, `src/probe.c:439–441`, and `src/runtime_thread.c:56–78`. Both producers retain first-PT_TLS values and size bounds; the loader admits align0 and nonzero powers1/2/4 as well as larger powers up to4096. Setter align0 substitutes16. Runtime computes offset and allocation, then converts/stores TCB before calling ARCH_SET_GS and assigning current. Thus the revised qualification reflects actual source ordering.

The following are source/model arithmetic with supplied metadata and type-alignment premises, not executed fixtures, observed addresses or successful undefined-behavior paths:

| Supplied inputs | Source-derived alignment consequence |
|---|---|
| filesz1/memsz1/align1, adequate image/readable template | Admitted; offset1, total257, allocation320. A64-aligned base+1 fails supplied type alignment8 before GS. This is case3's preserved negative. |
| filesz1/memsz1/align2 | Admitted; offset2, total258, allocation320. Base+2 can fail type alignment8. Admission alone is insufficient. |
| filesz1/memsz1/align4 | Admitted; offset4, total260, allocation320. Base+4 can fail type alignment8. Some other memsz values yield suitable offsets, so the repair correctly says these alignments can fail rather than universally fail. |
| case1 filesz8/memsz24/align0 | Setter substitutes16; offset32, total288, allocation320. Under supplied type alignment8, 64-aligned base+32 preserves typed alignment. |
| case1 filesz8/memsz24/align16 | Same safe arithmetic and type premise; bytes0..7 copy, bytes8..31 zero, TCB starts at32 under the additional defined-access premises. |
| case3 memsz65/align64 | Offset128, total384, allocation384. A64-aligned base+128 preserves64 alignment and supplied type alignment8. |
| case3 memsz65/align128, legal64-aligned base congruent64 mod128 | Offset128 preserves supplied type alignment8 but still fails requested128 alignment. This is a separate negative, retained alongside F1. |

Cases1/3 explicitly preserve suitable typed alignment as an example premise, not an installed ABI fact. Actual target `_Alignof(uint64_t)` remains UNKNOWN. The official C11 draft [N1570 section6.3.2.3 paragraph7](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf), already inspected for review r1, supplies the pointer-conversion condition; its additional candidate citation remains separate from the unchanged six mutable primary API descriptions and is not compiler/platform qualification. The repaired general conditional layout claim no longer permits a defined TCB-write inference from admission/allocation/GS alone. F1 is resolved without an upstream implementation change.

## Affected integration and reused limits

Actual r1→r2 delta is ten paths: five shared routing/registry records, dossier, RC-0029, frontier, author r2 copy and verbatim review r1 copy. Four shared files preserve exact r1 prefixes; removing only the r2 registry block recovers r1 registry bytes. Status appends consistently identify F1 repair and pending affected recheck/human editorial acceptance, with no premature PASS/root acceptance/runtime promotion. The source registry separates N1570 from its six API descriptions. Git whitespace check passes.

RC-0028 and author r1 are byte-identical. Only cases1/3 changed among the eighteen numbered rows; the other sixteen rows are byte-identical. The dossier source-inventory text is byte-identical. The r1 receipt for the145 protected base objects/modes, original file PR21 records, failed-usability links and Issue9 OPEN/NOT MET is reused; no changed path in this delta collides with that protected set. This review does not claim to rerun the author's full link/count/YAML checks or a complete source/API inventory. Mechanical checks bind identities and deltas; the direct source/phase comparison supplies F1's semantic recheck.

No changed interaction weakens the meaningful positive: matching successful host join, under correct API/ABI, host identity and ordered eligibility, terminates that one host thread. Stored result/key-tail guarantees retain ordinary-path requirements. Termination still does not establish guest resource retirement, transitive work or TLS/game fidelity. Borrowed template/readability/lifetime, original-game TLS/TCB/DTV/compiler conventions, actual GS/allocator/register outcomes, byte-rewrite instruction reachability, installed libraries/ABI, dynamic TLS/unload, cancellation/faults, HLE object/stop behavior and scheduler/hardware fidelity remain unqualified. Source/model, serialized, native-fixture and game claims remain separate; this package supplies only source/standards/API reasoning.

## Closure and next consumer

Same author and parent receive this frozen affected-recheck result. Parent owns final acceptance, integration and any publication. A later status-only delivery delta can be checked against this exact candidate while reusing unchanged technical evidence; new technical changes require affected recheck. Frozen r1 reports remain preserved.

Reviewer writes are limited to this new report. No descendants, background process or live owned handle remains. No candidate/canonical/source writer, upstream execution/build/script, fixture/thread test, register/syscall operation, private input/state/source, game/device/UI, reader retry, dependency installation, model route change, new topic/framework or external action occurred. Commands completed. Assigned Sol/high role is known; independently served-model telemetry, usage/tokens/cost and measured elapsed scope are UNKNOWN. No additive billing inference is made. Freeze and report SHA-256 are delivered separately, avoiding circular self-identity.
