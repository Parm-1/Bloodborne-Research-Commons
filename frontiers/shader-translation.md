# One shader translation question

BRC-SHADER-BUFFER-LOAD-01, 2026-10-13, proposed topic in [Issue #12](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/12). Read the [BUFFER_LOAD_DWORD dossier](../knowledge/buffer-load-dword-translation.md), [RC-0014](../claims/RC-0014-buffer-address-arithmetic.md) and [RC-0015](../claims/RC-0015-buffer-load-codegen.md) first. SOURCE_INSPECTED at bbport `3c57da4198ad62039f63f33bfd205b9916518acf`; technical review and editorial acceptance pending. No runtime authority or fresh-reader result is added.

**Next question:** does an authorized synthetic comparison of the aligned shortcut and forced general address path preserve the intended effective address at the U32 overflow boundary?

The [actual source counterexample](../knowledge/buffer-load-dword-translation.md#original-worked-examples-and-discriminators) is I=0x10000000, stride=16, offset zero. It predicts J=0x40000000 in the shortcut and J=0 in the general wrapped-byte formula; paging converts the former back to byte offset zero. These are source calculations, not observed results or an ISA defect determination.

A future consumer needs a pinned primary intended-ISA rule; exact raw fields, descriptor, stage and profile; one matched pair that changes immediate eligibility while preserving the resolved scalar value; active unpatched generated code; binding/table/trash identity and lifetime; and attributable result acquisition. The dossier specifies outcome branches and the one-pair stop rule. Missing any essential attribution gives UNKNOWN. No game shader, game data or upstream execution is authorized by this document. Do not expand to a suite, cache dossier or renderer survey from this frontier.
