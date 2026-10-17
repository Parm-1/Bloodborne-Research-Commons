# BRC-RWLOCK-01 independent affected recheck r2

2026-10-17. Actual trigger: parent activated the original uninvolved reviewer for the linked R1 premise repair. Reviewer did not author or substantially design either candidate. This is an affected-claim recheck, not acceptance or authority to integrate, publish, merge or execute. Candidate and canonical state were kept unchanged.

## Exact subject and frozen evidence

Commons branch research/brc-rwlock-01; repaired candidate commit `6eb12b55d538412f71775095a84c8fe9f040a1d1`, tree `8f79cf41fe465794e441618ee868907696c9c36f`; tag brc-rwlock-candidate-r2 dereferences to that commit. Reviewed predecessor remains `4c51611a55c4c38da2d53c5f5d4bbd218b10e327`, tree `1103eba1ab600ae5ac1117f5b6bf35cca6d81fee`, tag brc-rwlock-candidate-r1 unchanged.

Author repair report `/tmp/BRC-RWLOCK-01-AUTHOR-r2.md`: SHA256 `a5e83d5a62865bc631979e15fbda5077bfc64babdfc5345aaedf5f5d7a41825f`, 8945 bytes, mode 0444; exact public-copy bytes confirmed. Frozen author r1 remains SHA256 `5590f1ff716058aa0d9fb600c79366676cb7cd40d6811f3c5f233fead9eb3be5`, 10467 bytes, mode 0444; its candidate bytes are unchanged. Frozen independent review r1 remains SHA256 `4b2db89450ef5e646658d2124d5f0cb629fb9542a83f95724cf25beadcde986b`, 14773 bytes, mode 0444; its newly added public copy is byte-identical. Read back all three delivery copies and compared their candidate public content.

Primary source identity is unchanged: public bbport commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. Reuse r1's independent source/API review and preservation receipts. No new upstream/source-freshness query, source/API semantic re-audit, corpus-content audit or producer execution was needed for this qualification-only delta.

## R1 disposition: resolved

No remaining actionable finding in the affected delta. The repair changes the conditional contract's explicit premises, not the producer or its observed qualification.

The new common-contract section directly requires caller handle/alias slots disjoint from wrapper-owned Rwlock, Holder, registry and native-object storage. Accessed attribute/deadline bytes must remain readable and stable without concurrent mutation across their reads. It explicitly says registry locking does not validate overlap or snapshot/synchronize caller input bytes. The prior common conditions remain: valid/live/aligned typed backing and applicable conversions/SysV ABI, phase-applicable native initialization, successful ignored registry mutex operations, live pthread identities, complete wrapper-only use, ordered external slot/alias mutation, nonwrapping retention counters and normal cleanup without cancellation/fault/nonlocal exit.

Protected-application-data safety is separately conditional on relevant readers, writers and lifetime owners cooperating in their consumer access/lifetime protocol. The wrapper does not store or establish that protocol, and retiring the native object still does not retire caller data/storage. The new text does not assert that actual consumers meet these premises.

The internal-next output-slot overlap and unsynchronized busy-deadline mutation remain source-only exclusion countermodels, never defined expected-error positives or executed failures. This preserves the distinction between an omitted contract premise and a demonstrated algorithm/runtime defect.

## Affected phase interactions and propagation

- A1: explicit init's output publication requires disjoint caller storage; accessed attr pointer value requires stable readable backing. Phase-applicable native initialization still allows initially uninitialized output storage and does not introduce an old-*out read. Source A1 row is unchanged.
- A2: lazy slot-zero creation and later tombstone publication inherit disjoint storage. Requiring native initialization only where operations need it preserves lazy creation, raw-zero destroy and explicit reconstruction semantics.
- T1: the common contract expressly exempts paths that never access a deadline, including timed native try0 with NULL. RC-0044 and frontier repeat this carveout. It therefore does not accidentally require readable backing for an unused NULL deadline or turn invalid nanoseconds into mandatory EINVAL on the immediate-success path. Original T1 case row remains exact.
- T2/T3: the inheritance paragraph explicitly requires stable readable deadline bytes across every busy-path read. This addresses repeated nanosecond reads and later seconds/nanoseconds construction. Busy validation versus native absolute-deadline result remains unchanged; no native timed call or timeout is invented for invalid input. Early self-conflict and non-EBUSY try outcomes still bypass time access.
- D1-D3: disjoint output/alias storage applies to tombstone, explicit replacement and alias lookup implications. The caller's independent storage lifetime remains separate from native-object lifetime. Explicit replacement can still orphan a registered old object; no generation/ABA observation was added.
- RC-0044 and RC-0045 propagate disjoint/stable-access premises into their conditional statements; their limits keep application-data protocols separate. Frontier carries the premises into missing consumer evidence and future eligibility, explicitly excludes the countermodels and preserves the try0 carveout. Status text and report links describe repair/recheck pending at the frozen candidate phase; they do not pre-accept this review.

Strong actual retention remains intact. The entire dossier body from Producer/storage/callable route through diagnostics/lifecycle, before the conditional-cases section, is byte-identical to r1. This preserves admitted pre-native retention, native wait/attempt, deadline validation, native-success-before-bookkeeping, recorded-success ownership, any-Holder/inflight destroy rejection, and failed-acquire cleanup-before-guest-return distinctions. The new premises neither weaken this positive into a generic missing-lease assertion nor extend it to caller/thread/protected-data completion. The meaningful raw-field negatives and native-host-invalid-use exclusions from r1 still apply.

## Actual checks and preservation

Read the exact r1..r2 delta, repaired common contract, both claims, frontier, author repair report and five shared insertions. Independent checks confirmed:

- Exact 11-path delta: nine modified existing paths and two added reports. Candidate has 225 files. No additional path changed relative to the already reviewed predecessor; thus the original 213 protected base object/mode identities remain inherited without a repeated inventory audit.
- Removing each of the five complete marked rwlock blocks from r1 and r2 yields identical outside-block bytes. Together with r1's exact original-base recovery checks, all five original-base recoveries remain valid. Eventqueue, failed evaluations/evaluated heads and Issue9 history remain untouched; no fresh external Issue/PR status query was made.
- Ten complete source-matrix rows and all 16 complete case rows are byte-identical to r1, rather than merely sharing IDs. Counts remain A1-A3=3, L1-L4=4, T1-T3=3, U1-U2=2, D1-D4=4. The new inheritance paragraph is a prerequisite statement, not a seventeenth case.
- Frozen r1 author/tag identities and r1 review public-copy identity match the original pins. R2 author report pin, size, mode and public-copy bytes match parent delivery.
- Local-link scan of changed/new Markdown files returned 894 resolvable links and zero missing paths/fragments. This mechanical scan includes inherited links in the four large shared files; it is not 894 new/changed links or semantic re-review of their content. Meaningful new links route to the preserved review and author repair reports, and the new common-premise fragment resolves.
- Eleven unique rwlock registry keys remain within the bbport mapping: the original nine plus review-r1 and repair-r2 references. No full YAML parsing is claimed; constrained insertion/containment checks and the previously established unavailable-parser limitation are retained. No installation occurred.
- git diff --check r1..r2 returned 0, and Commons worktree was clean. Both candidate tags resolve to their exact frozen commits.

The reviewed evidence class remains SOURCE_INSPECTED with conditional source/model examples only. No serialized, native-fixture, game, scheduler, timing or usability qualification is added. Actual loaded caller/artifact, original ABI/layout, installed dependency, host-operation success, cooperating consumer protocol and runtime premises remain UNKNOWN unless supplied by separate attributable evidence. No absent runtime fact was converted into a success by this premise repair. This review does not freshly validate mutable API descriptions or installed artifacts.

## Handoff and resource closure

Only `/tmp/BRC-RWLOCK-01-REVIEW-r2.md` was written and frozen. No repository edit, publication, external contact, fixture/runtime/device/UI test, compiler oracle, source import/build/scripts, protected/private/game input, source-freshness query, framework/model shopping, spending, descendant, live process/tool handle or writer transfer exists. Tools completed and no timed experiment was performed. Usage/cost/served-model attribution and measured phase intervals remain UNKNOWN.

Return R1 resolved and this exact reviewed identity to parent. Root/owner acceptance, bounded status integration, publication and editorial merge remain their decisions; this recheck grants none. Original r1 records remain immutable. Any later correction requires a linked successor and an affected recheck only if its changed claims require one. Stop after frozen checked handoff.
