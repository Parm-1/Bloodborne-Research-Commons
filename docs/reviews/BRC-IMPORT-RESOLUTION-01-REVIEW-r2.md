# BRC-IMPORT-RESOLUTION-01 — independent affected review r2

Date: 2026-10-13. Same uninvolved reviewer, checking the author's linked F1 repair. This report supersedes the pending F1 disposition for the exact r2 candidate below; the original r1 report and original reviewed candidate remain preserved.

## Reviewed identity

Commons branch `research/brc-import-resolution-01`, tag `brc-import-resolution-candidate-r2`, commit `f898c04190fb5b12dee4b58ef07df9a1d5b5d556`, tree `ad94bd75904d6cd5ee0089be940540fcd050d3d5`.

Dossier SHA256 `9ed69e83d3cac3e4befca6ad9b03f154d13799a4192ea29c3688a6776a84971f`; AUTHOR-r2 SHA256 `8f52cae45da7faf3b9d15b52df109e57cc64e669ad8aa692a6d3b5eb64d003a4`. Original REVIEW-r1 SHA256 `bc5fac6528ccd8a0a2ba467d5b9291d7c84ce5a466402e20075141f26d20a0e3`; candidate copy is byte-identical to the frozen original.

Compared directly against r1 commit `8ee04c3f161d9b9c1e6daf0b3531c13c48aadee5`, tree `0051ed37f02ef420690e65cd951c4f201b4ebedd`. The three-path delta is the repaired dossier and added AUTHOR-r2/REVIEW-r1. RC-0018, RC-0019, frontier, registry and earlier records are unchanged. Candidate HEAD, tree and tag agree; checkout is clean.

Primary source remains public `deadinside28/bloodborne_pc@3c57da4198ad62039f63f33bfd205b9916518acf`. Independently refreshed affected working-byte identities: `src/probe.c` blob `75ead5c8ffd6955891e88c9741134c47059fc825`; `scripts/link_modules.py` blob `81f23fb42a8c856ea7a1e8a7f75f5aee5cbb6f65`. Both match the pinned objects; source HEAD and clean status agree. The unchanged r1 eighteen-blob inventory, preservation checks and unaffected semantic review are reused, not claimed as newly repeated.

## F1 closure and affected interactions

**F1 closed; no actionable defect in the affected repair.** Dossier line 31 now separates normally produced nonzero offsets from raw consumer validation. It correctly identifies that storing address zero leaves `bindings[index]` clear, allows a later same-index entry to pass the duplicate predicate, and leads zero entries to be treated as absent later. This follows [probe.c lines 443–458](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L443-L458), [placement checks lines 487–497](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L487-L497) and [selection lines 533–538](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L533-L538).

The revised ordinary fallback positive explicitly requires a nonzero binding, host result zero, enabled linked mode, matching kind and coverage. The normal-producer positive is also supported: a positive-sized prepared main image yields a positive aligned module base; indexed identities yield one emitted binding per entry, with export offsets added to that base ([link_modules.py lines 95–127](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/scripts/link_modules.py#L95-L127), [lines 182–206](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/scripts/link_modules.py#L182-L206)). This is explicitly conditional on normal valid producer output, not a claim that the linker authenticates arbitrary raw input.

The added raw-field row supplies applicable 4096-byte host pages and valid surrounding metadata premises. For a zero-base module of size 4096, two `(0,0,1)` binding triples satisfy the stated predicate and leave index zero absent for placement/fallback. Replacing the second address with covered executable offset 128 leaves that entry eligible for selected fallback under the stated gates. Reversing the decisive field order so the first entry is nonzero makes a later same-index entry fail the duplicate sentinel. The mapped checks' range arithmetic supports those conditional offsets ([probe.c lines 271–275](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c#L271-L275)). These source-reasoned positives and contradictory raw fields address the original finding.

The row expressly stops at predicate/selection behavior. It makes no serialized-fixture, complete-input validation, initializer-success, reached-call or runtime observation claim. Host selection still precedes linked fallback; zero capability/strict handling, early metadata checks, fallback-specific kind/addend coverage and later initialization phases retain their prior distinctions. Unchanged claim text does not reassert the repaired nonzero/uniqueness guarantee. The linked repair note and author receipt preserve pending acceptance and the prior review's narrower evidence class. Focused diff whitespace check passed.

## Limits, disposition and closure

Recommend this exact candidate for parent acceptance at SOURCE_INSPECTED scope, with the unchanged limits in REVIEW-r1. Review supplies no acceptance authority: parent integration/publication decisions and human editorial merge remain pending. Four accepted topics and Issue #9 OPEN/NOT MET are unchanged.

No upstream code or script was executed, no build or runtime was run, and no fixture, reader, game/protected input, source import or external write was created. This affected recheck does not independently establish ABI equivalence, host dispatch, feature correctness, native qualification or game fidelity. Registry parsing was outside this unchanged repair; the earlier parser-unavailable limitation remains.

Candidate and canonical records were not edited. The two checkouts remain clean and unchanged; original r1 evidence is retained. Only this separate public-safe report was written and frozen. No children, persistent process/session handles or runtime resources were created or remain owned. Usage, cost, served-model identity and measured review/author elapsed scope remain unknown; tool command timings are not total-work measurements.
