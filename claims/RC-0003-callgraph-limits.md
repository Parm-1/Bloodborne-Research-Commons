# RC-0003 — bbport's public callgraph scanner is candidate-oriented

**Level:** SOURCE_INSPECTED (public script), 2026-10-12.

At bbport commit `3c57da4198ad62039f63f33bfd205b9916518acf`, `tools/re/callgraph.py` reads ELF metadata and searches executable bytes for `E8/E9` relative-call/jump patterns whose computed target matches an unwind-derived function start. It summarizes calling functions and sites in a chosen target interval.

**Source:** [exact script](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py).

**Important limits:** Raw opcode-byte scanning is not complete instruction-boundary disassembly and cannot discover arbitrary indirect calls. Lack of a reported edge does not prove a function is unreachable. Scope any scan to an authorized executable and corroborate candidates with stronger static/dynamic observations.

**Next testable question:** Compare one small known function-range call relation against instruction-aware disassembly and one deliberately indirect call to map both positives and omissions.
