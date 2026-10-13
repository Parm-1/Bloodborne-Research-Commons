# BRC-AGENT-ENTRY-01 author receipt r8

**Scope:** the same-author repair of the affected continuation review r1 (F1 to F4). The predecessor is candidate r7, commit `ebef8306b79684e4b8ee88401328da2720e44e01`, tree `eea7cdb14727e01a8d8172482412014524890acd`. The repaired entry is candidate r8, commit `01ed1bbb5cae9398951617184cbec425de6bbcf6`, tree `dbd8e335c2c87994e5be86d13649f13328c89763`, tag `brc-agent-entry-candidate-r8`. The reviewed design r1 and its receipt are frozen and unchanged. This receipt records repair and checks only. It does not grade any reader, does not change any earlier grade, and grants no acceptance or publication authority.

## Repairs in r8

- **F1, producer semantics.** The texture section of [CONTINUATION.md](../CONTINUATION.md#texture-upload-readers-that-overlap) now separates five readers. Row B is a CPU hash-only job for a GPU-selected upload. Row B2 is the mode-2 inline untile and hash on the calling thread, which publishes no pool state and creates no queued job. Row C is the GPU read of imported guest source, and row D is the device-local route, whose untile reads scratch. The incorrect sentence that did not require a CPU reader is replaced by a statement that every GPU-selected upload has a CPU reader of guest memory in one of two forms. That statement covers only the selected GPU branch.
- **F2, worked example.** The example now compares finite 64-bit hash values, not bytes, and it states that the values are not an atomic content version. The limit separates the absent current lookup after a Surface reference is dropped from an attributably recorded completion for the same job, which would remain evidence. The example supplies no such record.
- **F3, task-entry status.** [README.md](../../README.md) and [START_HERE.md](../../START_HERE.md) each carry one plain current-status paragraph above their task material. It states partial editorial acceptance, the fixed fresh-agent criterion not met, and the open usability gate, and links the current entry status.
- **F4, design.** Design r1 is unchanged. [BRC-AGENT-ENTRY-01-PROSPECTIVE-EVALUATION-r2.md](BRC-AGENT-ENTRY-01-PROSPECTIVE-EVALUATION-r2.md), SHA-256 `ed1011e8813f2c4646449f0557685038b1f3f6d7f7d921ebf2bbe0b27dd47b7e`, binds the subject to the seven entry blobs of r8, closes the budget and the closure rule, separates the observation classes, and removes the discretionary repair clause.

## Source checks

In the read-only bbhost scratch at `566184a74f071166299bb656c4af479e5bbe2771`, the `src/host/textures.cpp` blob was verified as `54b61d74e06a3c124661b97aa58f092950befbab`. The ranges cited in the r8 text were read at that pin: `content_hash_of` at lines 634 to 666; `gpu_untile_plan` at lines 1010 to 1048; the `on_gpu` selection at lines 1115 to 1116; the mode-2 copy block at lines 1119 to 1129; the device-local route conditions at lines 1091 to 1097; the hash-only queue at lines 1131 to 1135; the batch branch at lines 1139 to 1145; the fetch at line 1165; the default settings at lines 984 to 1000; `run_prep` at lines 847 to 852; and `textures_before_submit` at line 3344. This is a bounded check of the cited statements, not a semantic review of the renderer.

## Checks

- `git diff --check` and `git show --check` are clean for r8.
- The three changed entry files have 44 relative links and anchors, with 0 errors.
- The r7 to r8 diff touches only `README.md`, `START_HERE.md` and `docs/CONTINUATION.md`. The seven r8 entry blobs are listed in design r2.
- Claims, knowledge dossiers, frontiers, the source registry, `AGENTS.md`, the evidence policy, `LICENSE`, the four-topic checkpoint table, `CORPUS_CHECKPOINT.md`, `SOURCE_REVIEW.md`, `SOURCE_FRESHNESS.md`, `llms.txt`, the frozen reports, prior receipts and prior tags are unchanged.

## Limits

No reader, task, live ref query, runtime process or source import was used. The design is not a commissioning decision. Model billing, token totals and elapsed durations are unknown, so this receipt makes no cost, speed or usability claim.
