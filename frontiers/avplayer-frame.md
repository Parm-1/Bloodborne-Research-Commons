# AvPlayer frame frontier — one pixel-reader decision

**2026-10-17 — Proposed/unmerged SOURCE_INSPECTED, BRC-AVPLAYER-FRAME-01, Batch04 [Issue #24](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/24). Independent source review, root acceptance and owner editorial acceptance/merge pending.**

Consumer: media/runtime maintainer selecting a safely owned copy or a separately justified retention/completion mechanism. [Dossier](../knowledge/avplayer-frame.md), [RC-0056](../claims/RC-0056-avplayer-frame-output.md), [RC-0057](../claims/RC-0057-avplayer-frame-lifetime.md), [author r1](../docs/reviews/BRC-AVPLAYER-FRAME-01-AUTHOR-r1.md). Public bbport `3c57da4198ad62039f63f33bfd205b9916518acf`; source-only, KNOWLEDGE_REFERENCE.

The invariant to preserve is the identity of one callback allocation and one content generation while every reader still needs it. Getter success copies metadata, not ownership; current retains storage until recycle/cleanup, and next success recycles before return. A false call alone can retain current only with actual ordering and no intervening lifecycle operation. Neither an active/paused/EOF/time field nor a worker's nonjoinable handle closes all readers.

The next missing premise is a **consumer-specific ordered reader endpoint** that completes before source recycle/free, together with demonstrated producer/getter/lifecycle ordering and valid extent/stride/callback premises. No actual public pixel consumer, runtime schedule or completion record is supplied. This package authorizes no target execution or synchronization/renderer design.

| Future authorized observation | Decision branch |
|---|---|
| A valid source frame is copied into consumer-owned storage while current is retained, all conflicting operations ordered, all requested bytes valid | Consumer can continue reading its own copy after player advance; qualify exact copied span/content/stride and copy completion, not full playback. |
| Reader completion is attributable to that allocation/generation and precedes every permitted recycle/free, with lifetime/ordering established | Reuse may be considered for that one endpoint; a generic GPU fence or unrelated worker join is insufficient. |
| Same p recurs after recycle or decoded linesize disagrees with width==pitch bulk premise | Reject pointer identity as content identity or general decoded-frame fidelity; retain A5/A15 countermodels. |
| Shared locks, queue flags, elapsed time or nonjoinable alone are offered | Premise unresolved; stop promotion. No defined concurrent-value/crash prediction. |
| Teardown can overlap escaped readers, detached work, callback reentry or unbounded joins | Keep lifecycle/retention DEFER/UNKNOWN until exact ownership and completion are established. |

Smallest falsifier for a claimed durable borrowed pointer: under a future authorized correctly ordered setup, retain metadata p for one generation, advance successfully, and establish a later decoder write to that same p before the supposed reader-completion boundary. This is a proposed observation, not an executed test or a fixture grant. A future successful copy does not repair source concurrency or qualify physical presentation.

Stop this outcome at frozen source candidate and parent-dispatched independent review; actionable findings go to this author in linked successor versions and the same reviewer for affected recheck. Stop rather than expanding into media input acquisition, decoder/native/allocator/GPU tests, source import, model shopping, a new reader/framework or a whole media audit. Full playback, media correctness, physical presentation and usability remain unqualified; Issue #9 OPEN / NOT MET and all frozen/failed/accepted history preserved. TLS PR #36 over #35/#34/#33/#32/#31/#30 is integration-only, not corroboration or merge acceptance.
