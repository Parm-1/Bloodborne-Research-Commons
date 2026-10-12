# RC-0003 — bbport's public callgraph scanner is candidate-oriented

**Level:** SOURCE_INSPECTED (public script, read but not executed), 2026-10-12. **Independently reviewed:** a bounded source/documentation review of candidate-r1 ([REVIEW-r1](../docs/reviews/REVIEW-r1.md)) confirmed the description except the scan bounds (repaired in r2); recheck of r2 pending. The script was not run by the reviewer either. "Candidate-oriented" is this repository's characterization of what the script can establish, not an upstream statement; the script's own docstring labels its output a direct call graph.

**Checked:** script read in full at the pinned commit; blob `034c98b92e163f21a17163c7daf0393e7c7b89dc`.

At bbport commit `3c57da4198ad62039f63f33bfd205b9916518acf`, `tools/re/callgraph.py` takes an ELF path and an address range `[LO, HI)`:

- it parses program headers, takes the first executable `PT_LOAD` segment as the code, and takes function starts and sizes from the `.eh_frame_hdr` search table and each FDE (the size is read at a fixed FDE offset, which presumes 32-bit pointer encodings; the script does not validate this);
- it tests the byte offsets from 0 through N-6 of an N-byte code image (the loop is `range(len(code) - 5)`, so offset N-5, the last possible five-byte instruction start, is never examined) for `0xE8` (call) or `0xE9` (jmp) followed by a rel32 operand, keeps the hit when the computed target is a function start inside `[LO, HI)`, and attributes the site to the function whose FDE range contains it;
- it prints the number of functions in the range, how many are called from outside, and the distinct outside callers; with an output path it writes per-function site and caller counts and a `.callers` file.

**Source:** [exact script](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py).

**Important limits:**

- Raw byte scanning is not instruction-boundary disassembly, so an `E8`/`E9` byte inside another instruction or an embedded constant can produce a false site. A hit also needs a valid function-start target and an FDE-owned source, which narrows but does not remove this.
- `E9` hits are jumps, so "callers" include tail-jump sources.
- Indirect calls and jumps, short and conditional jumps, calls into the middle of a function, and callees without an FDE entry are not found. A missing edge does not show a function is unreachable.
- Coverage is limited to the first executable segment, to functions the unwind table describes, and to offsets 0 through N-6 (the last five-byte instruction start is omitted; this is an upstream behavior, not something this repository repairs).
- The documented input (`out/eboot.elf`) is derived from a game executable. Scope any run to an authorized executable and corroborate candidates with stronger static or dynamic observations.

**Reuse disposition:** KNOWLEDGE_REFERENCE. bbport is declared GPL-2.0-or-later and vendors shadPS4 code ([source registry](../sources/projects.yaml)); no code is copied here.

**Next testable question:** Compare one small known function-range call relation against instruction-aware disassembly and one deliberately indirect call to map both positives and omissions.

## Revision notes

- **r1, 2026-10-12** (supersedes the wording of the seed commit; original: `git show seed-original:claims/RC-0003-callgraph-limits.md`). The seed's description was confirmed against the script. Changes: stated that the script was read and not run; made "candidate-oriented" an explicit characterization; added how function starts and sizes are obtained, the first-segment restriction, the tail-jump and missing-FDE limits, the input provenance, blob hash, reuse disposition and review status.
- **r2, 2026-10-12** (candidate-r2, linked to the reviewed candidate-r1, commit `c517ebd4758ddf1a920c50bda2e72dd580b7d0fa`; review finding 2 in [REVIEW-r1](../docs/reviews/REVIEW-r1.md)). r1 said every byte offset is tested. The pinned scanner ([line 37](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L37)) stops five bytes short of the end; the actual bounds are now described and the omission is listed among the limits.
