# RC-0011 — selected camera arms isolate named regions, not all state

**Level:** SOURCE_INSPECTED. **Checked:** 2026-10-12, bbhost `566184a74f071166299bb656c4af479e5bbe2771`, selected Linux/SysV offline `decomp_follow_camera` source; no execution or reproduction. Independent review pending.

The offline test clones each camera at case start, then runs original A before replacement B for 60 frames with per-frame GSM/shape snapshots and restoration, cleared effect records and re-fed mouse counts/predecessor flag. Character/params/world/image and helper state are shared. A failed camera-or-GSM gate copies only A camera to B; other failures do not resynchronize camera state, and the accumulated failure remains fatal.

**Primary sources:** [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L445-L558); [tests/decomp/follow_camera_test.cpp](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L558-L595); [src/engine/mouse_camera_step.h](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/mouse_camera_step.h#L67-L127). Full inspected bounds and source blobs: [dossier](../knowledge/original-code-differential-validation.md#inspected-source-bounds-and-identities).

**Meaningful negative (prospective, not executed):** Prospective fresh-versus-carried sequence replay and reversed arm order with identical explicit inputs can falsify isolation; unchecked shared mutations or counters are not proven absent by equal camera words.

**Exclusions:** Source control flow does not establish successful environment setup, path reachability, original-world collision behavior, library fidelity, game coverage or a runtime/adoption result. Exact equality and state limits belong to the [selected-pair contract](../knowledge/original-code-differential-validation.md#validation-contract--this-selected-pair); upstream game comments and run counts remain PROJECT_REPORTED.

**Ownership/reuse:** bbhost authors retain their source and declared GPL-3.0-or-later at the [existing registry scope](../sources/projects.yaml). KNOWLEDGE_REFERENCE; no third-party code copied. New claim; supplements RC-0002 without replacing its historical prefix.
