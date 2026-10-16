# BRC-AJM-BATCH-01 — linked initial-review completion r2

2026-10-16. This report-only addendum completes the initial independent review after parent steering arrived immediately following the r1 freeze. It is not a candidate repair, candidate recheck or acceptance. Preserve review r1 unchanged: SHA256 `55b990ef3e9e7a8db0d21fc6663f85543369bd9d8d3c6865b8dd6a0924c78ce2`, mode0444. Read both reports as one batched handoff.

The exact candidate remains Commons `e6eaa0d671be7beb70ca8c68ff734d4e0945a1ea`, tree `4b79af83097411f5c6c0770dfd1bd68e0404a931`, tag `brc-ajm-batch-candidate-r2`. Source remains bbport `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`, selected AJM blob `9d69d25112ebbfcdc6db3a920b14664a96f7593d`. Both worktrees remain clean and unchanged. The dependency identity, absent-artifact premise, preservation checks, limits and closure in r1 remain applicable.

## Additional affected field-applicability finding

**F3 — N3 must request the attempt-count field, not merely provide capacity.** Location: `knowledge/ajm-batch.md:92`. N3 supplies a sideband that “covers result, stream and multi-frame count” but does not explicitly require the producing flags. At the pinned `src/runtime_ajm.c:335`, the local frames counter increments once even on the failed first at9_frame; at`:359`, the raw8-byte multi-frame field is written only when RUN_MULTIPLE_FRAMES bit12 is set and room remains. Stream separately requires bit47 (`:346–348`). If bit12 is clear, a sufficiently large sideband alone does not cause the count field to be written; preexisting bytes at a guessed count offset can remain unrelated to local frames1. This is a conditional source/raw-field negative, not an executed decoder result. The absent qualified dependency/compiler artifact continues to prevent an established feasible full-path decoder case.

Minimum same-author repair: explicitly bind N3's requested stream and multi-frame flags plus its capacity/order. With format/gapless/codec-info requests absent, result8 + stream16 + count8 needs declared/actually backed32 bytes, and the emitted count is at offset24. Equivalent explicitly bounded field arrangements are sufficient. No source, encoded input, fixture or runtime test is requested.

Repair interaction: D1 requires bit12 clear; N3 requires it set to observe an emitted count, and N4 enables it to continue processing. S1 deliberately requests stream/format/gapless, with actual48/declared32 and no other fields, and must retain that ordering/capacity contrast. A blanket zero-unspecified-bits statement cannot replace these per-case requested-field premises or remove N3/N4/S1's explicit overrides. For N2/M1, the requested stream flag and no-initialization setup remain distinct requirements. Recheck only this affected flag/field interaction together with F1/F2 and their current claim/frontier references; reuse unchanged inventories and dependency analysis.

## Exact source-location corrections to r1

R1 F1's post-success single-frame break is at AJM`:337` (the following`:338` closes the loop). Its partial/room re-entry references`:326–332` remain correct. R1 F2's RIFF-before-initialized ordering is at`:328–329`, not its stated`:325–326`; initialization control is`:310` and the selected RIFF fmt reset is`:240` as stated. These corrections change locations only, not the source behavior or findings. They are preserved in this linked report rather than editing frozen r1.

## Disposition and closure

Recommendation remains return to the same author before conditional source-reference acceptance, now with F1–F3 batched. Parent should reactivate that owner for a linked r3+ candidate/report, then reactivate this same uninvolved reviewer for the bounded affected recheck. Parent owns acceptance/publication; human owns merge. Nothing here accepts or integrates the candidate.

Only the granted linked report was written; r1 and all candidate/source bytes were unchanged. No descendant, source execution, fixture, decoder/parser/pthread/syscall/native/runtime/device/UI/game test, encoded/private input, model/spending change or external publication occurred. No live owned process/session/child/fixture or unresolved writer remains. Usage/cost/served identity/measured phase interval UNKNOWN. R2 is frozen0444 before final READY with SHA256 returned outside its bytes.
