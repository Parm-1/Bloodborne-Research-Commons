# RC-0014 — the selected raw buffer address has branch-specific U32 arithmetic

**Atomic claim:** for a surviving ordinary BUFFER_LOAD_DWORD in pinned bbport, resource patching produces a descriptor-relative dword index with separate aligned-shortcut, general linear and swizzled U32 formulas. The shortcut is not unconditionally equivalent to shifting a wrapped byte result: I=0x10000000, stride=16 and zero immediate offset produce 0x40000000 in the shortcut and 0 in the general formula.

**Subject/version/platform:** bbport `3c57da4198ad62039f63f33bfd205b9916518acf`, vendored GCN-to-SPIR-V source with matching descriptor/profile/binding premises, supported host field layout and software Compute for add_tid. A geometry ring rewrite is excluded from the ordinary address claim.

**Evidence level/date/method:** SOURCE_INSPECTED, 2026-10-13. Producer, descriptor and decisive address/emitter bodies inspected at the exact pin; original hypothetical calculations checked by ordinary arithmetic scripts (MODEL/source reasoning). No upstream execution.

**Primary pinned source:** [MUBUF decode](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/shadps4/shader_recompiler/frontend/decode.cpp#L894-L957), [front end](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/shadps4/shader_recompiler/frontend/translate/vector_memory.cpp#L207-L273), [address calculation](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/shadps4/shader_recompiler/ir/passes/resource_patching_pass.cpp#L546-L636). Exact formulas, all input widths, phases, bounds/blobs and other consumers have one home in the [dossier](../knowledge/buffer-load-dword-translation.md#descriptor-identity-and-address-arithmetic).

**Meaningful negative:** the stated overflow pair falsifies unconditional formula equivalence. Original idxen/offen, swizzle, unaligned-byte and operand-encoding counterexamples discriminate inputs the producer actually uses; see [worked cases](../knowledge/buffer-load-dword-translation.md#original-worked-examples-and-discriminators).

**Exclusions/unresolved:** intended ISA correctness, active shader reachability, original-lane/EXEC fidelity, arbitrary descriptor discovery, cache reuse under changed descriptor fields, low-bit unaligned reconstruction, addr64/lds/tfe support and all execution are unqualified. No original AMD ISA source was inspected. Descriptor base is a binding premise, not part of this index. See the [one next question](../frontiers/shader-translation.md).

**Upstream ownership/license/reuse:** original bbport/shadPS4 authors, declared GPL-2.0-or-later lineage in the [registry](../sources/projects.yaml); KNOWLEDGE_REFERENCE. No upstream code copied or code-combination assurance.

**Reviewer:** pending uninvolved technical review; author does not approve this contract. Editorial acceptance pending; no reader test requested. [Author r1](../docs/reviews/BRC-SHADER-BUFFER-LOAD-01-AUTHOR-r1.md).

**Supersession:** none; new proposed claim in [batch Issue #12](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/12). Existing claims and history unchanged.
