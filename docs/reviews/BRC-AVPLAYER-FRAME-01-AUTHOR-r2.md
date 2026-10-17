# BRC-AVPLAYER-FRAME-01 — linked author repair r2

2026-10-17. **Proposed/unmerged SOURCE_INSPECTED. Independent review r1 found F1/F2; this author supplies the linked correction. Same-reviewer affected recheck, root acceptance and owner editorial acceptance/merge remain pending.** No self-approval, execution, publication or merge authority. This report accompanies `brc-avplayer-frame-candidate-r2`; exact commit/tree/tag and report SHA256/bytes are returned after freeze.

[Dossier](../../knowledge/avplayer-frame.md), [RC-0056](../../claims/RC-0056-avplayer-frame-output.md), [RC-0057](../../claims/RC-0057-avplayer-frame-lifetime.md), [frontier](../../frontiers/avplayer-frame.md), frozen [author r1](BRC-AVPLAYER-FRAME-01-AUTHOR-r1.md), frozen [independent review r1](BRC-AVPLAYER-FRAME-01-REVIEW-r1.md).

## Actual trigger and immutable evidence

Parent activated ordinary same-author linked repair for both findings, with no acceptance yet and same-reviewer affected recheck after parent pin verification. Consumer and source-only outcome remain the media/runtime maintainer's borrowed-video-pointer ownership/lifetime decision. No prior human request is reinterpreted as unanswered. This is the same bounded package, not a new source implementation or media campaign.

Frozen candidate r1 commit/tag `d3b14068a37b12d32c808410ee146e6b46c2fa89`, tree `dd0908f2926a3abf1b8a09608c7c3f00a8769aaa`, tag `brc-avplayer-frame-candidate-r1`, remains unchanged. Public author r1 and its temporary copy remain identical mode0444, SHA256 `13f228415d9a8d84ee0fba1878dbee149713c0ec4dbd59351f9e05bfc1563098`, 11097 bytes. Review r1 was copied verbatim under the permitted report grant: public/temporary SHA256 `4cddd9e1209a5b2d9cd88bbf972b6022dc6500088768e32d4cc9d2aca491c737`, 12752 bytes, mode0444. Its findings and original candidate remain historical evidence; this repair does not rewrite them.

Public bbport pin remains `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. Source is read-only. Every Git invocation explicitly names `/usr/bin/git -C` and the correct exact repository root; no Commons ref is queried in the source clone and no source fetch/update/currency query occurs.

## F1 — actual Stop return branches and deciding validator

The r1 author incorrectly interpreted the syntactic failure arm after source Stop as a reachable SetState(Stop) rejection. Read source `avplayer_state.cpp:281–295,407–417,512–579` against source Stop cleanup `avplayer_source.cpp:304–339` and public impl `avplayer_impl.cpp:213–217`. SetState calls IsStateTransitionValid; the latter specially handles Play/Pause/Jump/TrickMode/Buffering, while Stop reaches the accepting default at576–577. Under defined normally returning premises, post-cleanup rejection is unreachable.

Replaced A18 with the actual positive and contrary branches: live source, entry state other than Stop, source Stop true and normal callback/notification return reaches SetState(Stop), accepted state update and ORBIS_OK. Missing-source/already-Stop state rejection occurs before source call; no-joinable source false returns before source cleanup and before SetState. A17 retains its narrower source-early-return premise. No exception, corruption or undefined concurrent execution is used to manufacture a false post-cleanup return.

Dossier lifecycle paragraph, A18 and revision note now describe these branches. RC-0057 contract, negatives and revision note match; its primary links explicitly bind SetState407–417 and validator512–579. Dossier/registry source-bound lists add those two ranges in the existing state blob `c81f9e1c6631b9d564654333873c726e107c162d`. No source blob or existing claim ID changes.

The error branches do not themselves free buffers in that call. This is not a universal lifetime guarantee: a result cannot establish that earlier or intervening success/cleanup/destruction or excluded concurrent/external operations left an escaped pointer alive. The existing live same-source, actual ordering, no intervening lifecycle/success/external action and quiescent teardown limits remain explicit. Getter false-retention and worker-versus-external-reader completion boundaries are unchanged. Shared summaries state normal success/teardown can free and inspected errors precede that call's cleanup; they preserve those lifetime exclusions.

## F2 — raw timestamp selection and conditional rescale

Read the same selected helper `avplayer_source.cpp:642–655`. Selection starts at best_effort_timestamp, falls back to PTS only on AV_NOPTS_VALUE, and then to packet DTS only if still AV_NOPTS_VALUE. Missing/negative selection or nonpositive time-base denominator yields zero before rescaling; other values call av_rescale_q and only its positive return survives. The r1 missing/negative shorthand was too broad because missing best-effort alone need not select a missing value.

Replaced A22 in place with explicit scalar tuples, at time-base1/1000:

- `(AV_NOPTS_VALUE,42,AV_NOPTS_VALUE)` selects PTS42. Under successful compatible FFmpeg rational rescaling to1/1000, the millisecond result42 survives the positive clamp.
- All three fields AV_NOPTS_VALUE select missing and yield zero before rescale.
- `(-1,42,AV_NOPTS_VALUE)` selects negative best-effort and yields zero without falling back to PTS42.
- A nonpositive denominator also returns zero before rescale.

These are applicability branches inside one paper row, not executed AVFrames, samples or independent trials. The positive explicitly supplies successful compatible rescale behavior; no installed FFmpeg result is claimed. The exact cited [FFmpeg7.1 av_rescale_q API description](https://ffmpeg.org/doxygen/7.1/group__lavu__math.html) describes rational rescaling with nearest rounding. Equal input/output rationals leave the finite42 unchanged under that contract. This is one newly read decisive primary description on 2026-10-17; the five prior primary descriptions and unchanged producer/ABI/geometry/thread evidence are reused rather than re-audited. Exact documentation bytes are not frozen; installed library/compiler/ABI and successful decoding remain unknown.

Dossier producer paragraph, A22 and revision note now bind raw selection and positive-result clamp; RC-0056 negative/applicability note and direct timestamp-helper link match. Shared summaries and bbport registry identify the correction. Six primary description URLs replace the earlier five-count summary, while source blobs remain 21 and paper rows remain 23. Any timestamp result remains scheduling metadata and supplies no presentation, playback or reader-completion receipt.

## Affected checks and preservation

Original Commons base remains `6eebcfafc0f442cf4d5e97048dd96c0e9a2f42d7`, tree `0dd6bb29e5116ec8ba64a027695e5c26a6d22e2a`, 262 files. r2 modifies the four live topic documents and five marked shared insertions, adds this author r2 and the verbatim reviewer r1, and preserves public author r1 exactly. Against original base: 12 changed/new paths, 269 final files, no deletion; all 257 nonshared original base objects/working bytes/executable modes preserved. Removing the sole AvPlayer block from each shared file recovers all five complete original bodies. This includes predecessor status/history and every accepted/pending/frozen/failed artifact. No main or predecessor integration acceptance changes.

Temporary focused r2 checker reuses the established identity/navigation mechanics and adds exact frozen r1 candidate/tag/tree, public/temporary author r1 and public/temporary reviewer r1 byte/hash/mode checks, with an allowed r2-delta path set. It compares21 unchanged source blobs/working bytes and bounds, adding only the two deciding state ranges; this is identity verification, not a repeated semantic source audit. A18 and A22 were replaced, not appended:23 unique row IDs remain, zero executed cases. Eleven unique topic registry keys now include author r2/review r1; six primary URLs and21 source-bound entries are scoped under bbport. Newline/whitespace, added local link/fragment and exact shared-recovery checks remain mechanical evidence only. PyYAML is unavailable; scoped indentation/list/key checks do not claim a full YAML parse. No framework was installed.

Complete-candidate check passed: 12 changed/new paths; 262 base files; 257 protected original object/byte/mode identities; five complete shared-body recoveries; 21 source blob/working-byte/bounds checks; 23 unique paper rows and zero executed cases; 63 added local links/zero fragments; 11 registry keys, 21 bounds and six primary URLs; 269 final files. Frozen r1 candidate/author/review identity checks, final newline/whitespace and clean-source checks passed. Exact final pins accompany freeze delivery. The draft check passed 11 existing paths, 268 files, 257 protected identities, five shared recoveries, 21 source blobs/bounds, 23 rows, 49 local links/zero fragments, 11 registry keys/six primary URLs. Initial adaptation of the temporary checker incorrectly omitted all report paths in its pre-report expected set; that literal was corrected to omit only the not-yet-created r2 report. No frozen report/candidate/source bytes changed. No new semantic tests or unchanged decoder/copy/thread audit were performed.

## Authority and resource closure

The contract correction is F1 Stop-return reachability plus F2 raw-field applicability/compatible rescale premise. Parent is notified; author supplies evidence and does not approve its own correction. Parent verifies this frozen r2 identity and returns affected claims to the same uninvolved reviewer. Only after recheck and a fresh parent grant may final-status integration occur. Any later correction to this frozen report uses a linked successor; r1 candidate/tag/author/review remain immutable.

Reviewed/unmerged TLS PR36 over35/34/33/32/31/30 remains integration-only, not corroboration. Main `689e2e29ed67d1c4f5231a1254b93ffd88586bc8`, original protected history and Issue9 OPEN/NOT MET retain their prior dispositions. No new reader, usability retry, execution eligibility or merge/publication acceptance is supplied.

No descendants/reviewer activation, source fix/import, private/game/encoded/actual media/prepared image, generated fixture, upstream script/build, decoder/FFmpeg/compiler/allocator/pthread/native/syscall/runtime/GPU/device/UI execution, framework/model change, push/PR/issue/merge or external contact occurred. All commands complete, Commons/source cleanliness checked at delivery; no live process, tool handle or runtime/UI resource requires resumption. Author/review/repair/integration usage, cost and measured phase time remain unavailable/unknown. Stop at frozen r2 delivery for parent-routed same-reviewer affected recheck.
