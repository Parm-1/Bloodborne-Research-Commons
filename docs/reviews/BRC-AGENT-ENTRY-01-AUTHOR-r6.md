# BRC-AGENT-ENTRY-01 author receipt r6

**Scope:** the entry delta for the owner disposition on PR #10, which gave partial editorial acceptance at source and documentation scope and left the adequate-usability gate open. The predecessor is candidate r5, commit `4b3b259869cddc816057e0517d871ade67c1b21f`, tree `8cc78afa93d79403747792913f466c126a1e3d7e`, tag `brc-agent-entry-candidate-r5`. The entry delta is frozen as candidate r6, commit `1a571a25a0c5ec90b2b4b21913fc0961a33636bf`, tree `3f526441dbf82daebd746483caddeb68e60e885d`, tag `brc-agent-entry-candidate-r6`. This receipt was added in the later delivery candidate r7, whose entry blobs equal r6. It records no usability result, and it grants no acceptance or publication authority.

## Changes in r6

- [CONTINUATION.md](../CONTINUATION.md) gained two sections. [Texture upload readers that overlap](../CONTINUATION.md#texture-upload-readers-that-overlap) gives a per-reader table of completion observations, the qualified mode-2 case and the concurrent-reader rules. [Separating premises in a task answer](../CONTINUATION.md#separating-premises-in-a-task-answer) defines supplied premises, cited implementation facts and future execution facts, with one new hypothetical worked example.
- [CORPUS_CHECKPOINT.md](../CORPUS_CHECKPOINT.md) replaced its current entry-status section. The status is partial editorial acceptance with the usability gate open, citing the owner review. It keeps the three fresh-reader stages distinct with their existing grades, states that no stage passed, and says that no new topic or evaluation is commissioned. The shader question is recorded as a hypothetical scenario, not independent consumer demand and not selected research. The four-row technical table is unchanged.
- [SOURCE_REVIEW.md](../SOURCE_REVIEW.md) gained one appended section, `Entry-layer continuation r6, 2026-10-13`. All earlier bytes are preserved.
- [README.md](../../README.md) gained one non-affiliation sentence at the end of its Boundaries claims paragraph.

Unchanged from r5: `START_HERE.md`, `llms.txt`, `docs/SOURCE_FRESHNESS.md`, the claims, knowledge dossiers, frontiers, source registry, `AGENTS.md`, the evidence policy, `LICENSE`, the frozen fresh-reader and usability records, the earlier author receipts and source reviews, and all prior tags.

## Source check of the new explanation

The bbhost pin `566184a74f071166299bb656c4af479e5bbe2771` and the `src/host/textures.cpp` blob `54b61d74e06a3c124661b97aa58f092950befbab` were verified with `git rev-parse` in the read-only scratch copy. The cited line ranges were read at that pin: `run_prep` at line 847; its hash-only branch at lines 851 to 852; the GPU untile selection defaults at lines 984 to 1000; the route selection at lines 1091 to 1097 and 1115 to 1119; the hash-only queue at lines 1131 to 1135; the batch branch at lines 1139 to 1145; the device-local fetch at line 1165; the GPU untile plan at lines 1010 to 1048; and `textures_before_submit` at lines 3344 to 3346. The line ranges were checked for the cited statements. This is a bounded source check of those statements, not a semantic review of the whole renderer.

## Checks

- `git diff --check` and `git show --check` are clean for r6.
- Relative links and anchors in the four changed files resolve: 109 references checked, 0 errors.
- Diff size from r5: README 1 line changed; CONTINUATION 34 added; CORPUS_CHECKPOINT 12 added and 8 removed; SOURCE_REVIEW 4 added and none removed.
- The checkpoint table rows are unchanged, and the SOURCE_REVIEW prefix is byte-identical to r5.

## Design delivered with r7

The single prospective design is [BRC-AGENT-ENTRY-01-PROSPECTIVE-EVALUATION-r1.md](BRC-AGENT-ENTRY-01-PROSPECTIVE-EVALUATION-r1.md), SHA-256 `a720ea62d4426347d2023c7aa0363d814e31486c4c37cea40936c24636afab91`. It binds to the r6 entry blobs. It states the representational hypothesis, four falsifiers, a single-reader single-attempt design, reading bounds, a finite budget, grading categories and limits. It contains no task wording, answers, keys or scores, and no reader was commissioned.

## Limits

The owner review is cited from its public GitHub record and was not rechecked here. The entry is not published by this receipt. The usability gate is open. Model billing, token totals and elapsed durations are unknown, so this receipt makes no cost, speed or usability claim.
