# RC-0012 — selected kit and scanner have conditional address-point correspondence

**Level:** SOURCE_INSPECTED, 2026-10-12. bbport `3c57da4198ad62039f63f33bfd205b9916518acf` and bbhost `566184a74f071166299bb656c4af479e5bbe2771`; source read only. Independent source review and fresh-reader check pending.

bbport scanner reports ELF VAs without image identity checks. The selected bbhost kit adds `0x400000` to ELF starts, subtracts it for first-containing file-backed PT_LOAD lookup, and requires that actual loaded slide for `at()` to address loaded bytes. The general address helpers/allocator use actual runtime slide; a preferred base is not universal. Same-image point correspondence requires consumer-supplied original digest/build/view and reversible unambiguous segment mapping. Original-file bytes and relocated/patched/runtime views are distinct.

**Primary sources:** [scanner](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L10-L67), [kit](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L95-L166), [load](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L181-L224), [address helpers](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/addr.h#L5-L27), [allocator](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/core/memory.cpp#L17-L58). Exact blobs/bounds, domains, loader view and additional consumer: [guide](../knowledge/function-address-correspondence.md).

**Meaningful negatives:** original hypothetical digest or file-offset mismatch contradicts a same-image/mapping claim; absent digest or base is UNKNOWN. Missing unwind entry or different displayed base alone does not contradict an otherwise supported point conversion.

**Exclusions:** Not a logical-routine, extent-completeness, decoded-edge, reachability or replacement/runtime-equivalence result. No tool/image execution; hypothetical examples are not OWNED_TESTED. No supersession of prior findings.

**Ownership/reuse:** original authors retain declared GPL-lineage source; [existing registry/license scope](../sources/projects.yaml) unchanged. KNOWLEDGE_REFERENCE, no code copying. [Author r1](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r1.md); reviewer pending.
