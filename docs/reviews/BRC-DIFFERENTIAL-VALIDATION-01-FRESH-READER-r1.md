# BRC-DIFFERENTIAL-VALIDATION-01 — fresh-reader result r1

## Binding and scope

Read-only fresh-reader check of public PR [#6](https://github.com/Parm-1/Bloodborne-Research-Commons/pull/6), bound to requested head `097fee0f7a2df451d7cddd1a4499eaf727564e5a`. A live `gh pr view` read confirmed that exact remote head; no newer head was observed. The reviewed Commons dossier is `knowledge/original-code-differential-validation.md` at that commit (blob `1928a1eec5f55ec650044a01671bb8a6e02223b8`). External source references below are pinned to `droogie/bbhost@566184a74f071166299bb656c4af479e5bbe2771`.

No local Commons checkout, private project record, memory, binary, fixture, extracted code, executable, runtime, game, GPU, or upstream tool was used. No edits to candidates and no external writes/contact occurred. My evidence is public source reading only; author receipts of static checks and prior review reports were read as reports, not rerun or treated as producer evidence.

## Fresh-reader answer

If every selected frame compares equal, this pair has checked, under its own observation rules, selected camera bytes word-by-word, the 0x20-byte GSM region raw-byte-for-byte, ordered recorded collision questions, debug draw begin/matrix records and shape bytes, and the recorded free-camera-run outcome. The selected test’s frame gate is at `tests/decomp/follow_camera_test.cpp:552-558`; the loop’s outcome is accumulated in `bad` and remains fatal at `:584-595`. Its collision recorder captures filter/from/delta/radius and output-request flags (`:86-94`), while its synthetic answer derives a hit/fraction from those inputs (`:93-109`). The `void*` world argument is unnamed and unused in this stub (`:86`), so the test compares camera behavior under this synthetic collision response, not the game's collision world. Both arms bind `_FSin`, `atan2f`, and `tanf` to host implementations at `:412-418`; agreement therefore does not independently establish original library math.

The actual camera-word comparator does **not** preserve NaN payload identity. `tests/decomp/eboot_kit.h:105-112` accepts identical 32-bit words **or any two NaNs**. `follow_camera_test.cpp:355-364` applies it to four-byte words; `:552-555` applies it to debug matrices and shape. Cast records also canonicalize every NaN to `0x7fc00000` before equality (`follow_camera_test.cpp:75-82,86-94`). GSM alone is raw `memcmp` (`:557`). Thus payload-only changes can be invisible in the camera/draw/shape word relations and cast records, while payload changes in compared GSM bytes differ.

Still unverified are whether the shared collision stub returns the correct hit, fraction, or normal for real geometry/world state; whether host math matches the original system libraries; and behavior outside the selected synthetic inputs, patched/reference strata, and explicitly observed fields/state. Equal selected outputs do not establish all side effects, all game states, unrestricted replacement correctness, or gameplay fidelity. The source defines the checker, not successful execution or path reachability; no run was performed here.

## Proposed consequential falsifier

For a reached finite-output frame, keep the recorded cast question identical but use two independently specified world geometries whose correct hit/fraction differ. Compare each answer to an independent geometry oracle. If the current shared stub yields the same answer for both worlds (as its unused world argument predicts), while the oracle differs, this falsifies any inference that equal selected frames validate original-world collision behavior. This is prospective; it was not executed. A narrower comparator control is to alter only B’s finite final camera position by one bit and require `camera_same` to fail and `bad` to remain nonzero (`follow_camera_test.cpp:557-585`).

## Reading quality and next decision

The dossier answers the Issue #5 reader question and generally distinguishes selected-pair agreement from original-world/library fidelity. It supplies exact public paths and the consequential shared-stub limitation. I found no material navigation defect in the dossier’s links or its source pin. One wording precision: describing “per-quantity equality” in entry points is easy to overread as uniform bit identity; the dossier itself correctly gives the NaN exception and separates raw GSM comparison. The answer should retain that qualification whenever summarized.

Next decision: retain `KNOWLEDGE_REFERENCE` or choose a separately authorized consumer for this exact contract. Do not infer a runtime or game result from this reading.

## Closure

Remote head observed: `097fee0f7a2df451d7cddd1a4499eaf727564e5a`. All read commands completed; no persistent process or runtime handle remains. Usage and elapsed-time accounting were unavailable/unmeasured. This is a public continuation usability check, not an additional semantic approval stage.
