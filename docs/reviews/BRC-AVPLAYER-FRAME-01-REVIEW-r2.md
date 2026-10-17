# BRC-AVPLAYER-FRAME-01 — same-reviewer affected recheck r2

2026-10-17. **F1 and F2 resolved; no actionable finding in the affected repair and interactions.** This is an independent source-only recheck, not root acceptance, editorial acceptance, merge approval or runtime qualification. The reviewer did not author or substantially design either candidate and changed neither candidate nor canonical/source state.

## Exact subject and continuation

Actual trigger: parent activated the same reviewer's affected recheck of linked author repair r2. Historical human requests are not newly unanswered. Unfinished work at entry was the F1 Stop-return and F2 raw timestamp repair verification; it is complete within this review scope. Next consumer is the parent for its acceptance decision. No author repair or runtime work is activated by this result.

Commons root `/home/parm/Documents/GitHub/Bloodborne-Research-Commons`; exact candidate `8a6f83cbf053a979fc0af9e17f3f3e6a3b0661c9`, tree `36ef3d50cd5a71a9f46c9cbdb677a4ab7082ad0a`, tag `brc-avplayer-frame-candidate-r2`. Compared with frozen candidate r1 `d3b14068a37b12d32c808410ee146e6b46c2fa89`, tree `dd0908f2926a3abf1b8a09608c7c3f00a8769aaa`. Original base remains `6eebcfafc0f442cf4d5e97048dd96c0e9a2f42d7`, tree `0dd6bb29e5116ec8ba64a027695e5c26a6d22e2a`. Main remains `689e2e29ed67d1c4f5231a1254b93ffd88586bc8`.

Author r2 `/tmp/BRC-AVPLAYER-FRAME-01-AUTHOR-r2.md`: SHA256 `fceb3120026eeebd7c8353450d9c55c4387ea550295d2c4d1e826bf14aa08a8c`,10797 bytes,mode0444, identical to its candidate public report. Frozen review r1 `/tmp/BRC-AVPLAYER-FRAME-01-REVIEW-r1.md`: SHA256 `4cddd9e1209a5b2d9cd88bbf972b6022dc6500088768e32d4cc9d2aca491c737`,12752 bytes,mode0444, identical to the newly included public copy. Frozen author r1 remains SHA256 `13f228415d9a8d84ee0fba1878dbee149713c0ec4dbd59351f9e05bfc1563098`,11097 bytes,mode0444 and unchanged from candidate r1.

Source remains read-only `/tmp/brc-buffer-source-eBMo7q/upstream`, public bbport commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. All Git invocations explicitly used `/usr/bin/git -C` and the exact appropriate repository root. No Commons ref was queried in the source clone, and no fetch/update occurred.

## F1 resolved — actual Stop paths

Re-read exact affected state source281–295,407–417,512–579; source Stop304–339 and public implementation213–217. The transition validator's default accepts Stop. Under a live source, entry state other than Stop, source Stop true and normally returning callback/notification premises, the path clears retained buffers, accepts SetState(Stop), emits notification and returns ORBIS_OK. A state with no source or already Stop rejects before calling source Stop; the no-joinable source false branch returns before cleanup and before SetState.

The repaired dossier paragraph/A18, RC0057 and author r2 now distinguish those source-faithful positive/negative phases and expressly reject the unreachable post-cleanup SetState-failure interpretation. Dossier/registry include407–417 and512–579 in the same pinned state blob, and RC0057 links them. The revision note preserves the r1 error historically without retaining it as the current contract.

The repair preserves the useful boundaries: an early error does not itself free the buffer, but a return code grants no reader lifetime across independent/intervening lifecycle operations or excluded concurrency/external actions. Cleanup/destruction can still free borrowed storage. No stronger false-return retention guarantee, callback-reentry guarantee, worker termination guarantee or external reader completion is inferred. No new actionable finding in this interaction.

## F2 resolved — explicit raw fields and rescale premise

Re-read helper642–655 and its metadata propagation664–680 plus getter366–394. Selection is best_effort_timestamp, then PTS only on AV_NOPTS_VALUE, then packet DTS only if still missing. The missing/negative selected-value and denominator checks precede rescaling. Only a positive rescaled value survives.

Repaired A22 now supplies the discriminating raw tuples at time-base1/1000: `(AV_NOPTS_VALUE,42,AV_NOPTS_VALUE)` selects42; all-missing yields0 before rescaling; `(-1,42,AV_NOPTS_VALUE)` yields0 without PTS fallback. Nonpositive denominator also yields0 before rescaling. The conditional positive42ms follows from the explicitly supplied compatible successful rational-rescale API behavior, rather than a claim about an installed FFmpeg library. These are scalar paper branches, not executed frames or fixtures.

Independently read the added sixth primary description, [FFmpeg7.1 mathematics / av_rescale_q](https://ffmpeg.org/doxygen/7.1/group__lavu__math.html), especially the av_rescale_q operation and nearest-rounding equivalence. Equal input/output rational1/1000 preserves the representable integer42 under that description. Documentation bytes are not frozen. The other five primary descriptions are reused from review r1; no dependency version or installed ABI was assumed or newly qualified.

Dossier explanation/A22, RC0056 helper link/applicability note, author r2 and shared summaries agree. Timestamp remains scheduling metadata: default admission compares it to current time; non-Default bypass and old-buffer recycle order are unchanged. A positive or zero timestamp grants no decoder, presentation or reader-completion receipt. No new actionable finding in this interaction.

## Delta, preservation and check categories

Read the r1-to-r2 technical delta and author r2. Only A18/A22 differ among23 unique case rows; remaining rows and prior independent source analysis are reused. The change is11 paths versus r1: four live topic documents, five shared insertions, added author r2 and verbatim review r1. Against the original base there are12 changed/new paths and269 final tracked files, with no deletion. Tree-object/mode comparison preserves257 nonshared base objects; clean working state carries the earlier working-byte inventory forward. All five whole original shared bodies recover exactly after removing the sole topic insertion. The four shared navigation summaries have identical substantive prose after link-target normalization.

Temporary read-only metadata checks found no path-set, report hash/byte/mode, shared-recovery, case-ID or local-link-target error. Three affected source whole-file working blob identities (state/source/impl) match their existing pinned hashes. The21-source inventory is unchanged and reused; this was not another full decoder/copy/thread/source audit. Git diff --check passed. The two expanded state bounds and the new primary URL are present in dossier/registry, with six primary URLs and23 paper rows. Mechanical checks establish identity/navigation/scope, not semantic truth or executed tests. No full YAML parse or remote Issue/PR-state refresh was performed.

Status remains proposed/unmerged, affected recheck pending in the candidate's pre-review text, root acceptance pending and owner editorial acceptance/merge pending. Updating that status is a later parent-owned integration action. Issue9 remains OPEN/NOT MET in the preserved records; reviewed/unmerged TLS PR36 over35/34/33/32/31/30 is integration-only, not corroboration. All earlier frozen/pending/failed/accepted artifacts remain preserved. No authority or acceptance boundary changed.

## Limits and closure

Result: F1/F2 resolved for this exact linked candidate, with no further actionable finding in the affected contract, references, propagation, scheduling or lifecycle interactions. SOURCE_INSPECTED plus conditional scalar source/model reasoning only. Zero executed semantic cases, serialized probes, AVFrames/media fixtures, decoder/library/compiler/allocator/pthread/native/syscall/runtime/GPU/device/UI/game results. Missing installed ABI, actual ordering, valid allocation/geometry and external-reader completion evidence remain explicit limits. The source-only recheck supplies no playback, physical display or usability qualification.

No candidate/source/canonical edits, descendants, new reader, generated fixture, media input, build/upstream execution, publication, push, PR, issue or external message occurred. All commands completed; no live process, tool handle, descendant, test or UI resource is owned. Candidate/source cleanliness and identity are rechecked before freeze/delivery. Author/review/repair/integration usage, cost and measured phase time remain unavailable/unknown; no ledger or equivalence/savings inference. No model/tool handoff occurred inside a timed experiment because none was run.

Return to parent for its acceptance decision. This report is frozen mode0444 before READY; any later correction requires a linked successor. Exact SHA256/bytes are returned separately as delivery metadata. Review r1 remains immutable and applicable to its original subject; this r2 records only the affected repair and recheck.
