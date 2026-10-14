# Save commit: attribute replacement before asking about persistence

BRC-SAVE-COMMIT-01 / Batch03 [Issue #20](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/20) goal3; proposed SOURCE_INSPECTED, independent review and human editorial acceptance/merge pending. [Dossier](../knowledge/save-commit.md), [RC-0030](../claims/RC-0030-save-replacement.md), [RC-0031](../claims/RC-0031-save-success-limits.md) are the bounded contract.

Consumer: save-service maintainer selecting one complete-byte replacement or declared failure-model persistence decision. Reuse KNOWLEDGE_REFERENCE; do not rewrite the runtime foundation or infer authorization from this public record. One missing premise controls reuse: attributable unique regular copy/destination identity, exact complete-content sequence and, for durability, a separately checked persistence endpoint bound to the actual filesystem/device/failure model.

A future authorized non-game experiment could use original hypothetical bytes OLD/NEW and one stable normal write-capable CREATE|TRUNC copy, preserving identity and full count/offset/length receipts. Separate outcomes:

- Full intended content plus dirty captured close/filefsync0/rename0 and independent named-byte readback supports bounded replacement at that name. It does not establish power-loss persistence or close of earlier readers.
- Dirty1 or short/zero/error writes plus close0 without intended exact bytes falsify a full-request success predicate. No rollback follows from that earlier error.
- A failed checked file fsync skips rename; a failed rename requires filesystem-specific ambiguity handling. Preserve actual old/new bytes and errors rather than trusting the old-file log.
- Checked rename0 plus missing/failed directory-persistence endpoint leaves durability unqualified. A crash/power-loss claim requires its own authorized recovery evidence; sleep or cleanup success is not that evidence.
- Mount0 with failed file mapping/metadata, readonly-only printing, malformed suffix selecting a different exact route, multiopen overwritten bytes or retained descriptor after unmount falsifies a transaction/isolation/retirement predicate.

These are conditional design branches, not run fixtures or an execution grant. Expected bytes come from original controlled content and API/source branches, never original game assets or source comments. Preserve valid layout/readable spans, caller ordering, alias/temp uniqueness and actual installed ABI/artifact premises. Stop at source/documentation review, linked repair/affected recheck and one parent unmerged PR; no fixture mutation/syscalls/crashes, actual saves, game/runtime execution or fourth batch topic. Root owns integration/publication; human editorial acceptance/merge reserved. Issue #9 remains OPEN/NOT MET; failed usability links and all peer technical evidence unchanged.
