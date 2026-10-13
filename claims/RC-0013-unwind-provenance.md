# RC-0013 — selected unwind producers differ in validation and do not resolve routine identity

**Level:** SOURCE_INSPECTED, 2026-10-12. bbport `3c57da4198ad62039f63f33bfd205b9916518acf` and bbhost `566184a74f071166299bb656c4af479e5bbe2771`; source read only. [Independent source review](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md) found no actionable finding; parent accepted the source/documentation contract. [Public fresh-reader result](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r1.md) is complete and parent-accepted at reading scope, with [linked r2 wording clarification](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r2.md).

The scanner assumes fixed header/FDE layout and maps FDEs through its first executable segment, then sorts `(start,size)` tuples. The kit uses file-backed PT_LOAD lookup, checks selected header encodings and FDE begin agreement, and retains table order. Neither validates all extents or resolves duplicate/overlap identity. Their range signedness differs (scanner signed 32-bit, kit unsigned 32-bit). A compatible unwind extent is narrower than a logical routine or complete function inventory.

**Primary sources:** [scanner parsing/owner/output](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L10-L67), [kit segment/read helpers](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L41-L71), [kit function producer](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L137-L166). Exact source bounds/blobs and parsing comparison: [guide](../knowledge/function-address-correspondence.md#what-the-function-producers-actually-validate).

**Meaningful negatives:** original hypothetical duplicate starts, overlapping predecessor ranges, conflicting extents, unrecognized/truncated metadata and alternate segments falsify unqualified identity/coverage claims. Equal validated points with unequal extents conflict for extent, without automatically rejecting the point correspondence.

**Exclusions:** Kit count/completeness comments remain PROJECT_REPORTED. No general malformed-ELF qualification, decoded coverage, decompilation percentage, game observation or upstream repair. No tool/image execution; examples are hypothetical source/arithmetic reasoning.

**Ownership/reuse:** original authors retain declared GPL-lineage source; [registry](../sources/projects.yaml) unchanged in license scope. KNOWLEDGE_REFERENCE; no code copied, prior findings preserved. [Author r1](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r1.md); [independent review](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md) complete at source/documentation scope.

## Linked integration r2 — 2026-10-12

Status-only successor to frozen r1 (`6810b6704b5ae75d0c4108521c949d41dbb22e49`); technical claim, negatives, exclusions and source pins are unchanged. [Author r2 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r2.md). Fresh-reader work remains pending.

## Final integration r3 — 2026-10-12

Status-only successor to frozen r2 (`790ff6608cae66f8e73519932b51e4b7282c06e0`); technical claim, negatives, exclusions, source pins and prior notes are unchanged. Reader r1 and its linked r2 boundary-wording clarification are integrated verbatim; source/reader acceptance adds no execution evidence. [Author r3 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r3.md).
