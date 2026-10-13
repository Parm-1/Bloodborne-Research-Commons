# BRC-AGENT-ENTRY-01 author receipt r3

**Scope:** final entry-stage integration after the frozen r1 independent review and the affected r2 recheck. The predecessor is candidate r2, commit `81f8103c468a5128c1e102e580edfbae85f7b97d`, tree `f6c53487f120f77703d29e5bd1b882388348e91f`, tag `brc-agent-entry-candidate-r2`. The parent accepted the repaired r2 at source-inspected documentation and editorial scope. The cross-topic fresh-reader usability check is pending. This receipt does not confer usability, publication, runtime, game or acceptance authority.

## Integrated reports

Both reviewer reports were copied verbatim from their temporary sources, and each source hash was checked before the copy. A byte comparison of each copy against its source passed.

| Repository file | Source file | Expected SHA-256 | Verified copy SHA-256 |
|---|---|---|---|
| [BRC-AGENT-ENTRY-01-REVIEW-r1.md](BRC-AGENT-ENTRY-01-REVIEW-r1.md) | `/tmp/BRC-AGENT-ENTRY-01-REVIEW-r1.md` | `fe4ec0c48035c779f6f4d35ed3dcb6cc9ba2a1fd1456f42e3da18a015bb47046` | `fe4ec0c48035c779f6f4d35ed3dcb6cc9ba2a1fd1456f42e3da18a015bb47046` |
| [BRC-AGENT-ENTRY-01-REVIEW-r2.md](BRC-AGENT-ENTRY-01-REVIEW-r2.md) | `/tmp/BRC-AGENT-ENTRY-01-REVIEW-r2.md` | `75f1202a77891dc271d2d81fa3a6e6936e7ce62aa03853387614fc8f775f5006` | `75f1202a77891dc271d2d81fa3a6e6936e7ce62aa03853387614fc8f775f5006` |

## Status integration

- [CORPUS_CHECKPOINT.md](../CORPUS_CHECKPOINT.md) gained one entry-stage paragraph that links the r1 review, the r2 repair, the affected recheck and the source-review history. It states that the fresh-reader usability check is pending.
- [SOURCE_REVIEW.md](../SOURCE_REVIEW.md) gained one section, `Entry-layer review history, 2026-10-13`, that links both reviewer copies with their hashes and this receipt.

No other existing text changed. The task-first README, START_HERE, llms.txt, continuation protocol and freshness procedure are byte-identical to candidate r2.

## Frozen and accepted content

Compared with candidate r2, the accepted AGENTS, CONTRIBUTING, LICENSE, claims, knowledge, frontiers, sources, evidence policy, license proposal, publication check, drafts and GitHub configuration paths are unchanged. The earlier author receipts `BRC-AGENT-ENTRY-01-AUTHOR-r1.md` (`8b1f8ee4572f9cab08c859bb410a73845eedc1a93f85b56f58e01f80df659db7`) and `BRC-AGENT-ENTRY-01-AUTHOR-r2.md` (`6ca6d4bcbde564765795b54940050b0d03dccb1438030d7df7b9093849f46237`) are byte-identical to their committed versions. Relative to the baseline `74779fb1001ebbf82fc65fc399ab3ea44227c964`, the entry-stage changes under `docs/reviews` are additions only.

## Protocol boundary

No protocol, question, key or pre-reader material was opened, copied or integrated. The copied reviewer report records the hashes of those artifacts for provenance only, and this receipt does not reproduce or read their content. The reader's answers and scoring remain outside this receipt until the original reader result is frozen and separately reviewed.

## Checks

- The two reviewer copies match their expected SHA-256 values and are byte-identical to their source files.
- Relative Markdown links and anchors in the changed status files, both reviewer copies and this receipt resolve.
- `git diff --check` is clean after normalizing the final newline in the source-review section.
- No YAML was edited or parsed, and no runtime, remote-ref query, push or external write was performed.

Model billing, token totals and elapsed duration are unknown, so this receipt makes no cost, speed or usability claim.
