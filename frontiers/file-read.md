# File-read frontier — one attributable asset-I/O decision

Proposed SOURCE_INSPECTED BRC-FILE-READ-01, checked2026-10-14; independent review pending. [Dossier](../knowledge/file-read.md), [RC-0026](../claims/RC-0026-file-path-descriptor.md), [RC-0027](../claims/RC-0027-file-read-outcome.md), [author r1](../docs/reviews/BRC-FILE-READ-01-AUTHOR-r1.md). Batch03 [Issue #20](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/20) goal1; one proposed PR, owner editorial review reserved. Public source pin and exact blobs/bounds are in the dossier.

The controlling premise is attributable path/open/descriptor/attempt identity and destination lifetime for one actual consumer. A textual translation, reusable guest fd, pre-note or count does not supply that premise. Reuse the namespace and synchronous read mechanism as KNOWLEDGE_REFERENCE; DEFER asset/content correctness, sandbox, concurrent descriptor lifetime or device-visible completion inference. Full save commit proof is queued separately.

A future experiment, only if the actual target's records authorize its inputs and execution, would bind one unambiguous mapping and harmless known regular file, exact opened description/guest slot, eligible destination span, requested offset/count, every attempted raw host result/errno, later helper result with diagnostic/handler ordering, post-return bytes, and close/reopen order. Freeze expected bytes from that independent input, not from the observer. No experiment is executed or authorized here.

Outcome branches:

- Full or short positive final transfer matches known bytes at the attributable offset: supports that bounded host-object transfer; original asset correctness still needs original provenance/format premises.
- Zero at nonzero count and independently attributable regular-file EOF: supports EOF for that call; zero count, stale descriptor or unidentified file cannot do so.
- Correct bytes with absent/clipped notifications: separates transfer from coverage/device visibility; use the unchanged memory dossier for the selected hook predicates.
- EFAULT/error or close/reopen gap: preserve all attempts, raw syscall errors, later helper/adapted results and accesses; exact error attribution needs errno preservation through diagnostics/retry touches/handlers. Do not infer unchanged buffer/position, cancellation, old incarnation or rollback from the return.
- Different host object, mapping/truncation/case ambiguity, ABI/span fault or missing invocation identity: rejects application of the positive to that consumer rather than declaring the entire source mechanism unknown.

The smallest discriminating comparison is read(size64)->7 versus a full64 result at the same independently bound input, with pre-note64 and post-note7/64 distinguished. For identity, serial openA/close/openB reusing guest3 falsifies fd-as-incarnation without invoking undefined concurrent C behavior.

Stop rule: this commission ends after bounded source review, ordinary linked repair/affected recheck and parent one-PR delivery. Missing target authority or one required identity/span/dependency premise stops any future dependent execution. No protected data, actual assets/saves, game/runtime/device/UI work, new reader evaluation, framework or upstream execution is part of this package. Both usability results remain NOT MET; Issue #9 remains OPEN. No source/documentation result qualifies autonomous continuation or target runtime.

## Linked r2 repair — 2026-10-14

[Independent review r1](../docs/reviews/BRC-FILE-READ-01-REVIEW-r1.md) and its [linked qualification correction r2](../docs/reviews/BRC-FILE-READ-01-REVIEW-r2.md) are preserved verbatim. [Author repair r2](../docs/reviews/BRC-FILE-READ-01-AUTHOR-r2.md) addresses F1 current-errno versus raw syscall error and F2 explicit pre-request/post-positive spans; affected same-reviewer recheck pending. Review r2 retracts r1's universal16KiB VMA-edge rationale while retaining the phase-premise finding. No runtime or original-asset result is added. Earlier r1 remains recoverable at tag `brc-file-read-candidate-r1`.
