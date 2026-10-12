# RC-0010 — skip, setup failure and selected comparison success are separate

**Level:** SOURCE_INSPECTED. **Checked:** 2026-10-12, bbhost `566184a74f071166299bb656c4af479e5bbe2771`, selected Linux/SysV offline `decomp_follow_camera` source; no execution or reproduction. [Independent r1 review](../docs/reviews/BRC-DIFFERENTIAL-VALIDATION-01-REVIEW-r1.md) supports this principal claim; the [affected r2 recheck](../docs/reviews/BRC-DIFFERENTIAL-VALIDATION-01-REVIEW-r2.md) resolved the linked override-control finding with no remaining actionable finding in affected scope. Parent accepted the source/documentation contract; the [public fresh-reader result](../docs/reviews/BRC-DIFFERENTIAL-VALIDATION-01-FRESH-READER-r1.md) is complete and parent-accepted at reading scope, without execution evidence.

The kit exits 77 before selected comparison for missing/unreadable or wrong-hash input; CMake marks 77 as a skipped test. Loading/eligibility/binding rejection exits 1; a reached unbound function import aborts. The selected test returns zero only with no failed frames and nonzero mouse-turn, held-frame and Original-tuning counters. Zero differences alone are insufficient.

**Primary sources:** [tests/decomp/eboot_kit.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L95-L109); [tests/decomp/eboot_kit.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L181-L204); [tests/decomp/eboot_kit.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.cpp#L86-L90); [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L369-L418); [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L588-L595); [CMakeLists.txt](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/CMakeLists.txt#L472-L488). Full inspected bounds and source blobs: [dossier](../knowledge/original-code-differential-validation.md#inspected-source-bounds-and-identities).

**Meaningful negative (prospective, not executed):** A skip with no frames, guard rejection, fatal import and accumulated finite-output mismatch must remain distinguishable by phase, diagnostic and final outcome; none is comparison acceptance.

**Exclusions:** Source control flow does not establish successful environment setup, path reachability, original-world collision behavior, library fidelity, game coverage or a runtime/adoption result. Exact equality and state limits belong to the [selected-pair contract](../knowledge/original-code-differential-validation.md#validation-contract--this-selected-pair); upstream game comments and run counts remain PROJECT_REPORTED.

**Ownership/reuse:** bbhost authors retain their source and declared GPL-3.0-or-later at the [existing registry scope](../sources/projects.yaml). KNOWLEDGE_REFERENCE; no third-party code copied. New claim; supplements RC-0002 without replacing its historical prefix.

## Integration r3 — 2026-10-12

Status-only successor to frozen r2 (`0ff4736d06cc895381c846767e8849bcb350fcd6`); technical claim, negative, exclusions and pins are unchanged.

## Final integration r4 — 2026-10-12

Status-only successor to frozen r3 (`097fee0f7a2df451d7cddd1a4499eaf727564e5a`); technical claim, controls, exclusions, source pins and prior revision notes are unchanged. Reader acceptance is public source reading only.
