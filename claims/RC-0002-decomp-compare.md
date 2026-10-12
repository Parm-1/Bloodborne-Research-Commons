# RC-0002 — bbhost documents original-code differential testing

**Level:** PROJECT_REPORTED for the method and results in `docs/decomp.md`; SOURCE_INSPECTED for the helper interface in `tests/decomp/eboot_kit.h`. **Independently reproduced here:** NO. **Independently reviewed:** a bounded source/documentation review of candidate-r1 ([REVIEW-r1](../docs/reviews/REVIEW-r1.md)) found one inaccurate paraphrase in this claim (repaired in r2); the same reviewer rechecked the repair and found no remaining finding ([REVIEW-r2](../docs/reviews/REVIEW-r2.md)). Nothing was reproduced.

**Checked:** 2026-10-12, both files read at the pinned commit; blobs `3ce60ba7f09b1401631f9567dba26e1af028fa6b` (decomp.md) and `3efca4382246527daa6d5d31f5a1d36b41ee1ec6` (eboot_kit.h).

At bbhost commit `566184a74f071166299bb656c4af479e5bbe2771`, `docs/decomp.md` describes two checks of a game function rewritten as C++ (stated target: the game's 1.09 executable):

1. **Offline test:** the test loads the user's executable, runs the original function's own machine code beside the rewrite on generated inputs, and compares them bit for bit.
2. **In-game compare mode** (`BBHOST_DECOMP_COMPARE=1`): the original and the rewrite are compared while the game runs. The document says a function becomes the default once an in-game session (the document calls it a world session) compares with zero differences and a session with the replacement in place performs within noise of one without it ([lines 287-289](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md#L287-L289)). Its tables report per-function case and call counts with zero differences; these are the author's figures, not reproduced here.

`tests/decomp/eboot_kit.h` declares the helper for check 1. It maps the 1.09 executable (SHA-256 checked) at `0x400000`, relocates it, moves its TLS reads, turns every import into a trap that names itself (except the C library memory and string functions, which are the host's), makes the calling thread a guest thread (TLS block, console MXCSR and x87 control word), and does not run the game's static constructors. A test skips with exit code 77 when the executable is missing or is not 1.09. `stub()` and `bind()` replace game functions or imports that a test cannot set up.

**Sources:** [method](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md); [helper interface](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h).

**Important limits:**

- "Without the game" means without running a game session. The test still executes the user's own decrypted game code, so it needs a lawfully obtained executable and, under this repository's rules, explicit authorization from the actual project owner.
- A stub that both versions call can hide missing behavior (the document describes such stubs for param lookups and heap searches).
- `same_float` treats any two NaNs as equal, whatever the payload; the header gives operand-order differences as the reason.
- A skipped test (exit 77) establishes no comparison. Neither a source comment nor a skip is a game proof, and zero reported differences cover only the generated inputs and sessions the author ran.
- The rewrite is applied only when the executable's SHA-256 matches the 1.09 build, so results do not transfer to other builds.

**Reuse disposition:** KNOWLEDGE_REFERENCE for the method. bbhost is declared GPL-3.0-or-later; no code is copied here.

**Next testable question:** For one eligible pure game function, specify matched inputs, state isolation, a falsifying wrong-output case and the exact equality rule before reusing a differential runner.

## Revision notes

- **r1, 2026-10-12** (supersedes the wording of the seed commit; original: `git show seed-original:claims/RC-0002-decomp-compare.md`). The seed's facts were confirmed. Changes: level restated as PROJECT_REPORTED + SOURCE_INSPECTED with the artifacts each applies to; distinguished the offline test from the in-game compare mode instead of one merged description; added the executable-checked, 1.09-only and stub details; removed "CI skip" because the cited sources do not mention CI (replaced by "skipped test, exit 77"); added blob hashes, reuse disposition and review status.
- **r2, 2026-10-12** (candidate-r2, linked to the reviewed candidate-r1, commit `c517ebd4758ddf1a920c50bda2e72dd580b7d0fa`; review finding 1 in [REVIEW-r1](../docs/reviews/REVIEW-r1.md)). The adoption rule in r1 gave only the zero-difference condition; the pinned document also requires the replacement session to perform within noise of one without it. Both reported conditions are now stated. They are the author's reported rule, not reproduced here.
- **r3, 2026-10-12** (candidate-r3, final integration). Review-status line updated to the completed affected recheck ([REVIEW-r2](../docs/reviews/REVIEW-r2.md)); the claim body, level, pins and exclusions are unchanged from r2.

## Implementation extension, 2026-10-12 — BRC-DIFFERENTIAL-VALIDATION-01 r1

The entire earlier record above is preserved. New implementation inspection of the stateful selected pair is in the [dossier and reusable contract](../knowledge/original-code-differential-validation.md); [RC-0009](RC-0009-camera-equality.md), [RC-0010](RC-0010-differential-outcomes.md) and [RC-0011](RC-0011-camera-state.md) are atomic SOURCE_INSPECTED findings. This extends the earlier pure-function next question to the commissioned stateful camera case; it does not reproduce or promote historical PROJECT_REPORTED numbers.

Implementation-specific qualification of the earlier header paraphrase: the kit's zeroed TLS/TCB and GS stand-in setup runs only in default GS mode, and allocation/protection/GS installation success is not fully checked. FS=0 receives no kit TCB setup. The selected test's camera/draw/shape equality accepts two NaN-shaped four-byte words regardless of payload, its cast recorder canonicalizes NaNs, and its GSM comparator remains raw bytes; “bit for bit” is not an unrestricted payload-fidelity claim for this pair. Its references include host imports, shared collision/debug stubs and separately named deliberate update-site patches. A skip remains no comparison. Independent review and fresh-reader check of this new extension are pending, separate from the completed seed review.
