# BRC-DIFFERENTIAL-VALIDATION-01 — affected independent recheck r2

Date: 2026-10-12. Same uninvolved Sol/high reviewer. Linked successor to frozen independent r1 report, SHA-256 `3ee97030ffa22e7551570a3dc6361eea916e98f155c8ed63a8209cc3b86372fd`. This report is frozen at delivery; corrections require a linked successor.

## Exact subject

Candidate commit `0ff4736d06cc895381c846767e8849bcb350fcd6`, tree `e78b00c937da4c6d5b150bca19c774a320c0a482`, tag `brc-differential-validation-candidate-r2`; dossier `knowledge/original-code-differential-validation.md` blob `16b8eef81c8c2bf9cb6b3dd3f78dca8990565886`. Author r2 receipt blob `9e50b59c9032d0915634f6913fd5a0fd02828330`, SHA-256 `60b84d3110a31fe254e007d3a2c5c4bc7dc8fea93750576198ede12d0ae09ee3`. All independently match the clean checkout and frozen delivery pins.

Reviewed delta is from candidate r1 `229e3158b10764c671580a90a1c6a8296d6b5297`. The integrated independent r1 report is byte-identical to the original frozen report and has its commissioned hash. Public source remains `droogie/bbhost@566184a74f071166299bb656c4af479e5bbe2771`.

## Result

**F1 is resolved; no remaining actionable finding within this affected recheck.** The matrix, wrong-effect case, contract stop rule, RC-0009 and frontier now distinguish a discriminating override omission from an already-sentinel input. They require identical non-sentinel +0x14 pre-arm bytes and actual original-arm post-state showing -1 consumption, then unchanged B override bytes with equal camera results. The replacement's sentinel write is expressly insufficient to prove original behavior. Already-sentinel omission is classified as non-discriminating rather than as a comparator failure.

Re-read decisive actual source: [generator lines 291–304](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L291-L304), [snapshot/restore, capture and raw GSM gate lines 509–558](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/follow_camera_test.cpp#L509-L558), and [replacement consumption lines 532–550](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/decomp/camera/follow_camera.cpp#L532-L550). With different pre-bytes and original post-consumption evidence, unchanged B bytes necessarily differ from A's four captured bytes and the raw comparator detects them; camera equality does not mask that difference. The 90% sentinel generator case explains why the added prerequisite matters. These are source deductions and prospective controls, not reproduced executions.

Adjacent frontier wording now correctly says two-NaN camera-word payload differences are accepted by the declared word relation while payload-fidelity remains unqualified. This aligns with the existing comparator source assessment; it changes no equality operation. Existing original/patch modes, common stubs, state-restoration limits, skip/setup/trap/mismatch distinctions, branch participation limits and upstream adoption policy are unchanged and reuse r1 review. No full inventory or unchanged suite was repeated.

## Delta and mechanical checks

Inspected all 11 changed/added documentation surfaces for affected wording, version/status consistency and report integration: dossier, RC-0002/0009/0010/0011, frontier, START_HERE, llms, SOURCE_REVIEW, author r2 receipt and copied independent r1 report. No source registry/YAML change appears. Independent Git whitespace and 11-text UTF-8/no-BOM/no-NUL/no-CR checks pass; entire RC-0002 r1 prefix is preserved; the full source-bounds/identity section is byte-identical to r1. The unchanged 20-source identity inventory and prior closed research artifacts retain their r1 review scope. Author r2 link/citation counts remain its own static-check receipt, not independently executed semantic controls.

The repair narrows prospective-control applicability. It does not change the research question, producer/comparator, source pin, evidence levels, execution restrictions, license, ownership or authority. Mechanical next integration may copy this frozen report verbatim and update existing pending affected-recheck status in a linked successor; preserve prior reports/history. Separate fresh-reader exercise and consequential parent acceptance/publication remain outstanding, outside this reviewer's work. No review result grants acceptance or runtime authority.

## Limits and closure

This recheck is source/documentation-only. It supplies no model fixture, serialized-output, compiled/native/extracted-code/game/GPU result, original binary evidence, live branch receipt, actual consumption execution, world/library fidelity, order-isolation trial or performance measurement. Missing execution evidence remains outside the source-only commission, rather than a new acquisition prerequisite.

Candidate and public upstream checkouts stayed clean at the exact identities during final checks. Only this reviewer-owned successor report was written. No candidate/canonical edit, private BBPC/memory/other-chat evidence, binary acquisition, upstream tool/script execution, compile, fixture/native/game/GPU operation, source import, host/security/license change, spend, third-party contact, external write or child dispatch occurred. All commands completed; no persistent process/tool handle or shared runtime resource remains. Original author retains sole repair/integration writer; parent retains acceptance/publication. Review/repair/integration token costs and whole-review elapsed duration are unavailable/unmeasured. There was no timed experiment.
