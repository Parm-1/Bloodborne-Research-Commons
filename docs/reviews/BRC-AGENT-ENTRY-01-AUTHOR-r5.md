# BRC-AGENT-ENTRY-01 author receipt r5

**Scope:** final entry-stage integration after the frozen source recheck r4 and the entry-stage usability records. The predecessor is candidate r4, commit `4989ad73f991e15986f92bed007b12d2db1d322f`, tree `8c5a80ad4a8f4df3187994f77207ae2473b26c35`, tag `brc-agent-entry-candidate-r4`. The parent accepted the entry as a source-and-documentation entry at its reviewed scope only. The fixed whole usability criterion is not met. This receipt records integration and checks only. It makes no claim of adequate usability, semantic test success, causal improvement or broader qualification.

## Records integrated

Each record was copied under its existing filename into `docs/reviews`. Each source file's SHA-256 was checked against the expected value before copying, and each copy was compared byte-for-byte with its source.

| Record | SHA-256 |
|---|---|
| `BRC-AGENT-ENTRY-01-REVIEW-r4.md` (source recheck r4) | `fb4db6b1954ca98791544e425da2514715d6e61d4e459b91407e68503e6d01de` |
| `BRC-AGENT-ENTRY-01-USABILITY-PROTOCOL-r1.md` | `0863c3ae933ef0911bc6592347946676408c73cd8eceb6ea6370cf9ebd16bbef` |
| `BRC-AGENT-ENTRY-01-USABILITY-QUESTIONS-r1.txt` | `cdce023fe73f3d74b551e014aa3493d4b785096c94ddf76c8b5a5daaecb554aa` |
| `BRC-AGENT-ENTRY-01-FRESH-AGENT-r1.md` | `937e14eeaecdd1071ccdd2bb211307c8af6705cf587685aa0efcad28e5aa9479` |
| `BRC-AGENT-ENTRY-01-FRESH-AGENT-r2.md` | `8352cb54950e6ed21d1a19c1e20c8b1942dade449936fc41f9854c7a87747283` |
| `BRC-AGENT-ENTRY-01-FRESH-AGENT-r3.md` | `8faa6fc581de8b116d60643aa0f957e7e95412b4bd8e5042576cd9dc0cb77bb0` |
| `BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r1.md` | `b46d37f24345e5e5cc9d49141c0de2cc05f2712dcae7540bc704052c2bcdc8b4` |
| `BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r2.md` | `9e74400bdf64272c2f6643f13e90f1c070717c55013ee4cd4dcaba14c2852998` |
| `BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r3.md` | `f2fecc2229bfb93a6484a2d75d292fc9f540404c5f6b3d0a1edbc755fb311495` |

The copies are verbatim. Their relative links are unchanged, and none of them contains a relative Markdown link.

## Changes

- [CORPUS_CHECKPOINT.md](../CORPUS_CHECKPOINT.md): the pending cross-topic procedure paragraph and the earlier pending entry status were replaced by one current entry-status section. It records the accepted source-and-documentation scope, the three fresh-reader stages kept separate, the unmet whole criterion and the one conditional next gap. The four-row technical table is byte-identical to r4.
- [SOURCE_REVIEW.md](../SOURCE_REVIEW.md): one appended section, `Entry-layer final integration, 2026-10-13`, lists the copied records with their hashes. It states that the earlier pending wording is historical and superseded by the checkpoint. The earlier bytes of the file are preserved as a prefix.
- This receipt, added under `docs/reviews`.

Unchanged from r4: `README.md`, `START_HERE.md`, `llms.txt`, `docs/CONTINUATION.md`, `docs/SOURCE_FRESHNESS.md`, the claims, the knowledge dossiers, the frontiers, the source registry, `AGENTS.md`, the evidence policy, `CONTRIBUTING.md`, `LICENSE`, and the frozen author receipts r1 to r4 and source reviews r1 and r2.

## Checks

- The nine copies match their expected SHA-256 values, and each is byte-identical to its `/tmp` source.
- The checkpoint's four-row technical table and the earlier bytes of `SOURCE_REVIEW.md` are byte-identical to r4.
- Relative Markdown links and anchors in the changed status files and this receipt resolve, including the new checkpoint and source-review anchors.
- `git diff --check` is clean.
- The changed paths relative to r4 are the two status files, the nine copies and this receipt.
- No live ref query, YAML edit, runtime, source import, reader rerun, push or external write was performed. No private or protected material was added.

## Limits

The reader results are reading results at the stated scope, not blinded, randomized or statistical measurements. The Question 2 reasoning failure and the Question 3 partials remain visible in the records. The pull request for the source-and-documentation entry is pending a Research Director editorial decision. Model billing, token totals and elapsed durations are unknown, so this receipt makes no cost, speed or usability claim.
