# RC-0012 — selected kit and scanner have conditional address-point correspondence

**Level:** SOURCE_INSPECTED, 2026-10-12. bbport `3c57da4198ad62039f63f33bfd205b9916518acf` and bbhost `566184a74f071166299bb656c4af479e5bbe2771`; source read only. [Independent source review](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md) found no actionable finding; parent accepted the source/documentation contract. [Public fresh-reader result](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r1.md) is complete and parent-accepted at reading scope, with [linked r2 wording clarification](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r2.md).

bbport scanner reports ELF VAs without image identity checks. The selected bbhost kit adds `0x400000` to ELF starts, subtracts it for first-containing file-backed PT_LOAD lookup, and requires that actual loaded slide for `at()` to address loaded bytes. The general address helpers/allocator use actual runtime slide; a preferred base is not universal. Same-image point correspondence requires consumer-supplied original digest/build/view and reversible unambiguous segment mapping. Original-file bytes and relocated/patched/runtime views are distinct.

**Primary sources:** [scanner](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L10-L67), [kit](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L95-L166), [load](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L181-L224), [address helpers](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/addr.h#L5-L27), [allocator](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/memory.cpp#L17-L58). Exact blobs/bounds, domains, loader view and additional consumer: [guide](../knowledge/function-address-correspondence.md).

**Meaningful negatives:** original hypothetical digest or file-offset mismatch contradicts a same-image/mapping claim; absent digest or base is UNKNOWN. Missing unwind entry or different displayed base alone does not contradict an otherwise supported point conversion.

**Exclusions:** Not a logical-routine, extent-completeness, decoded-edge, reachability or replacement/runtime-equivalence result. No tool/image execution; hypothetical examples are not OWNED_TESTED. No supersession of prior findings.

**Ownership/reuse:** original authors retain declared GPL-lineage source; [existing registry/license scope](../sources/projects.yaml) unchanged. KNOWLEDGE_REFERENCE, no code copying. [Author r1](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r1.md); [independent review](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md) complete at source/documentation scope.

## Linked integration r2 — 2026-10-12

Status-only successor to frozen r1 (`6810b6704b5ae75d0c4108521c949d41dbb22e49`); technical claim, negatives, exclusions and source pins are unchanged. [Author r2 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r2.md). Fresh-reader work remains pending.

## Final integration r3 — 2026-10-12

Status-only successor to frozen r2 (`790ff6608cae66f8e73519932b51e4b7282c06e0`); technical claim, negatives, exclusions, source pins and prior notes are unchanged. Reader r1 and its linked r2 boundary-wording clarification are integrated verbatim; source/reader acceptance adds no execution evidence. [Author r3 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r3.md).
