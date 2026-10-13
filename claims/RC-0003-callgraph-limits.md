# RC-0003 — bbport's public callgraph scanner is candidate-oriented

**Level:** SOURCE_INSPECTED (public script, read but not executed), 2026-10-12. **Independently reviewed:** a bounded source/documentation review of candidate-r1 ([REVIEW-r1](../docs/reviews/REVIEW-r1.md)) confirmed the description except the scan bounds (repaired in r2); the same reviewer rechecked the repair and found no remaining finding ([REVIEW-r2](../docs/reviews/REVIEW-r2.md)). The script was not run by the reviewer either. "Candidate-oriented" is this repository's characterization of what the script can establish, not an upstream statement; the script's own docstring labels its output a direct call graph.

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
- **r3, 2026-10-12** (candidate-r3, final integration). Review-status line updated to the completed affected recheck ([REVIEW-r2](../docs/reviews/REVIEW-r2.md)); the claim body, level, pins and exclusions are unchanged from r2.

## Correspondence extension — 2026-10-12

**SOURCE_INSPECTED; BRC-FUNCTION-CORRESPONDENCE-01 r1.** Entire baseline prefix above is preserved. Reread the same pinned script in full; no execution or new scanner coverage finding is claimed. New cross-tool interpretation: its starts/sites/callers and LO/HI are ELF VAs, with no digest/base conversion. It sorts `(start,size)` tuples; duplicate starts survive in the range list while `dict(funcs)` retains the last sorted size. Ownership uses the last predecessor from `bisect_right`, checks only that selected end, and does not resolve overlaps. These are record/attribution rules, not logical routine identity.

The [output code](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L50-L67) counts all retained E8/E9 site occurrences, distinct inside/outside caller-start sets per target, and the outside caller union across targets. Range entries preserve duplicates. Optional per-function lines print only the first 20 sorted outside callers; `.callers` writes the full union. Without an output path only the aggregate is printed, despite the broader docstring description. No opcode split is printed. No callers does not establish unreachability or completed decompilation.

The [correspondence guide](../knowledge/function-address-correspondence.md) supplies conditional joins, incompatible/unknown cases, original hypothetical arithmetic and exact source bounds; [RC-0012](RC-0012-address-coordinates.md) and [RC-0013](RC-0013-unwind-provenance.md) distinguish point conversion and extent provenance. [Author r1](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r1.md) records the source-only checks; independent review pending. Prior scanner limitations, review history, ownership/license and testable question remain unchanged.

## Correspondence linked integration r2 — 2026-10-12

The [independent r1 source review](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md), SHA-256 `8ed8721985cfa77dd331c181e7be7f654bdd6104ca1f74aa6ec93b61bf886109`, is integrated verbatim: no actionable finding; parent accepted the source/documentation contract. [Author r2 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r2.md) records focused mechanical checks. Entire prior prefix, technical findings/examples/contract, source identities and all frozen reports are preserved. Fresh-reader validation remains pending; no execution claim or authority is added.

## Correspondence final integration r3 — 2026-10-12

The [public reader r1](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r1.md) at PR 8 head `790ff6608cae66f8e73519932b51e4b7282c06e0` and [linked reader r2](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r2.md) are integrated verbatim, SHA-256 `f12ec0e1c58251993f015846cf336ea7cdf401f5b85f9f1b92ccf81a7baec499` / `2197184cf6309b53bd36cc0e6cc00953c68d42d5e8865aa35e7c6e2c0fb1cd19`. Parent accepted the reading result with its wording qualification: only N−5 is a valid complete five-byte start omitted; N−4 through N−1 cannot fit one. Guide/RC-0003 were already correct; no technical repair. [Author r3 receipt](../docs/reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r3.md) records final focused status/report checks. Source review and reader work are complete at their separate stated scopes; entire prior prefix, technical content, source identities and frozen reports remain unchanged. No execution claim or authority is added.
