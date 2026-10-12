# RC-0009 — selected camera equality is quantity-specific

**Level:** SOURCE_INSPECTED. **Checked:** 2026-10-12, bbhost `566184a74f071166299bb656c4af479e5bbe2771`, selected Linux/SysV offline `decomp_follow_camera` source; no execution or reproduction. Independent review pending.

The offline follow-camera test applies identical-bit-or-two-NaN equality to every four-byte camera, submitted-matrix and shape word; cast records canonicalize float NaNs before ordered field equality; GSM uses raw byte comparison. There is no finite-value tolerance. Signed-zero and opposite-infinity encodings differ; NaN payload identity is excluded only in the applicable word/cast comparators, not in GSM.

**Primary sources:** [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L75-L117); [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L355-L365); [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L543-L558); [tests/decomp/eboot_kit.h](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h#L105-L112). Full inspected bounds and source blobs: [dossier](../knowledge/original-code-differential-validation.md#inspected-source-bounds-and-identities).

**Meaningful negative (prospective, not executed):** A finite camera output bit difference, missing cast or changed override byte must fail its applicable gate. A NaN payload-only camera word difference is intentionally accepted; the same raw GSM change is not.

**Exclusions:** Source control flow does not establish successful environment setup, path reachability, original-world collision behavior, library fidelity, game coverage or a runtime/adoption result. Exact equality and state limits belong to the [selected-pair contract](../knowledge/original-code-differential-validation.md#validation-contract--this-selected-pair); upstream game comments and run counts remain PROJECT_REPORTED.

**Ownership/reuse:** bbhost authors retain their source and declared GPL-3.0-or-later at the [existing registry scope](../sources/projects.yaml). KNOWLEDGE_REFERENCE; no third-party code copied. New claim; supplements RC-0002 without replacing its historical prefix.
