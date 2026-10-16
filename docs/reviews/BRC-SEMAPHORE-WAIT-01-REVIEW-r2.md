# BRC-SEMAPHORE-WAIT-01 — independent affected recheck r2

Date: 2026-10-16. Recommendation: **NO REMAINING FINDING** in F1 and its affected interactions. The parent may consider conditional SOURCE_INSPECTED acceptance and activate the existing author for final evidence/status integration. This review does not itself accept, integrate, publish, merge or qualify execution.

## Exact identity and prior review

Independently verified clean Commons HEAD `1bd3b33aea68d047937362ad52bdaca7834adbeb`, tree `2a39a41a69ea987d387c70eb05276e890098d441`, tag `brc-semaphore-wait-candidate-r2`, on the same research branch. Author r2 `/tmp/BRC-SEMAPHORE-WAIT-01-AUTHOR-r2.md` equals the public docs/reviews copy; both are mode0444, SHA256 `501f021e8c21eb5870415818a1ac7c4486fd2e3382a99893ee5f377f60085e46`.

Frozen r1 tag still resolves to candidate `4d15c0e8916942988ce1253d551d017d025cef63`. The original independent [review r1](BRC-SEMAPHORE-WAIT-01-REVIEW-r1.md), retained at `/tmp/BRC-SEMAPHORE-WAIT-01-REVIEW-r1.md`, equals the new public copy; both are mode0444 and retain SHA256 `0578541b20eef3de1070e48ca37fb3e033f80c240dc0afe5a3ff96399b3c55dd`. Its whole-source/host-description review, twenty conditional cases, eleven source-blob checks, protected baseline comparison and explicit limits are reused unchanged. This is the same uninvolved reviewer; I did not author the candidate or repair.

## F1 resolved against the producer

The sole technical edit at `knowledge/semaphore-wait.md:35` now requires capability mask `0x1` (bit index 0) to be set, separately requiring a function rather than data request. Read the actual pinned source again: `runtime.c:70–73` stores flags and tests `flags & 1`; `204–211` tests `capabilities & 1` before an early-return data branch; `239–240` reaches the semaphore resolver on function dispatch. Thus flags1 satisfies this capability predicate, flags2 alone fails it, and nonzero is_data cannot reach semaphore dispatch. This resolves the ambiguity from review r1 without changing admission semantics.

The unchanged `runtime.h:13–16` supplies the SysV annotation and resolver declaration. `tests/test_sema.c:14–35` retains matching function-pointer types, runtime_start(1), function requests with0, and the contrary data request. These are source declarations/call sites, not executed ABI or runtime evidence. The rest of the dossier paragraph still distinguishes the bridge/public source test from original-game invocation and keeps actual original caller arguments/order/ABI fidelity UNKNOWN. Retained correct-ABI/storage/host-operation and other defined-behavior premises are unchanged; neither the repair nor its report promotes evidence level or authority.

Source identity remains clean commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. No source was changed or executed, and no new upstream freshness query was made. No unchanged cases, host-description fetches, or old-topic audit were repeated.

## Repair preservation

Independent object/mode comparison found all173 other r1 entries unchanged. The only modified existing path is the dossier, whose complete r2 bytes equal r1 bytes with exactly the single identified admission phrase replaced. The two additions are author r2 and verbatim review r1. Consequently all20 case rows, both claims, frontier, five shared entry/registry files, author r1, prior technical evidence and failed usability records remain unchanged. Original baseline protection and insertion-only recovery conclusions therefore retain their r1 scope. Current pending/unmerged statuses, Issue9 OPEN/NOT MET and both failed results remain preserved; no live GitHub state query is claimed. Git whitespace check passed. No extra semantic repair or required evidence is outstanding for F1.

## Closure and next consumer

Only this linked `/tmp` report was written and frozen mode0444. Commons candidate/canonical checkout and public-source checkout remain clean and unchanged; no descendants, live process/tool session, thread, fixture, test display/UI/device or source-execution resource was created. No runtime/native/pthread/syscall/game test, upstream script/build/execution, acquisition, reader retry, source import, model change or external action occurred. Implementation/review/repair/integration token usage, served-model telemetry, cost and measured elapsed intervals remain UNKNOWN; no ledger or cumulative accounting inference was created.

Return to the parent for conditional acceptance and activation of the existing author for the already granted final status/evidence integration. The author must freeze and deliver its successor before notice; parent owns acceptance/publication and human owns merge. Frozen r1/r2 artifacts remain immutable. Any report correction requires a linked r3+ rather than an in-place edit.
