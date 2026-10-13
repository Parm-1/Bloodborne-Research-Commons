# BRC-IMPORT-RESOLUTION-01 — author repair r2

Date: 2026-10-13. Linked successor to frozen candidate r1 `8ee04c3f161d9b9c1e6daf0b3531c13c48aadee5`, tree `0051ed37f02ef420690e65cd951c4f201b4ebedd`. Candidate tag: `brc-import-resolution-candidate-r2`. Exact head/tree/dossier/report identities are returned after commit; this receipt is part of the frozen candidate and avoids circular self-identity.

## F1 repair and unchanged contract

[Review r1](BRC-IMPORT-RESOLUTION-01-REVIEW-r1.md), SHA256 `bc5fac6528ccd8a0a2ba467d5b9291d7c84ce5a466402e20075141f26d20a0e3`, is copied verbatim. The reviewer found that the raw binding consumer checks an address-valued duplicate sentinel without explicitly rejecting zero addresses. This author re-read the actual producer placement/emission and probe metadata, binding, placement and fallback predicates at unchanged public bbport `3c57da4198ad62039f63f33bfd205b9916518acf`.

The [dossier](../../knowledge/import-resolution.md) now distinguishes the normally produced positive-offset binding from the raw zero-sentinel limit. It states that zero can pass for a valid zero-base module, leaves the duplicate sentinel clear, and is treated as absent later. The existing selected-fallback row now requires a nonzero binding. One new source-reasoned row covers zero-first duplicate entries, a subsequent valid nonzero offset, and the contradictory first-nonzero repeated-index rejection. Host-page and otherwise-valid surrounding metadata premises are explicit. No serialized fixture was created or executed, and no full-input or initializer success is inferred.

This changes only the overbroad consumer-validation wording and its affected worked case. Other technical text, claims/frontier, source matrix/pins, license caveats, original AUTHOR-r1, original candidate/tag and all prior evidence remain unchanged. Independent affected recheck and parent acceptance are pending; author validation grants neither.

## Focused checks

Final check: 3 changed/added texts; 94 r1 files unchanged byte-for-byte; 9 relative references; zero relative anchors; 68 pinned citation occurrences at 42 distinct source locations; 18 matching dossier source blobs; 12 conditional reasoning rows; zero reported errors. Counts cover the complete changed documents, including the verbatim reviewer copy, rather than new-only references. The scope check permits only the dossier and the new AUTHOR-r2/REVIEW-r1 files. It verifies the original report and unchanged candidate files against frozen r1, the exact reviewer-copy hash, the dossier diff's bounded repair, UTF-8/link/anchor/source-bounds/blob checks and git whitespace. Unchanged r1 receipts retain their original scope; no upstream resurvey, runtime test, reader evaluation or repeat semantic review is claimed. Source-registry bytes are unchanged, so its earlier manual-check and parser-unavailable limit remain.

## Resource closure and stop rule

All commands completed synchronously. No live process, shell handle, child, build, upstream execution, runtime/game/GPU resource, source import, private evidence, external write or model change was created. Source checkout stays read-only and clean. Parent commissions the same uninvolved reviewer's affected recheck. Stop at this frozen repair; any later correction uses linked r3 or later. Usage, cost, served-model identity and measured elapsed-time telemetry remain unknown/unmeasured.
