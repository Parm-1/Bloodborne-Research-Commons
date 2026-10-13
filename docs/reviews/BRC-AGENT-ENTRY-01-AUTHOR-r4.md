# BRC-AGENT-ENTRY-01 author receipt r4

**Scope:** a narrow navigation and freshness clarification of candidate r3, commit `a969ab69263dd87c8c5a7845536f999a76182796`, tree `3ac09f408ed3026a07c1f2d6658eea22645be69f`, tag `brc-agent-entry-candidate-r3`. It came from an independent, private usability review of the entry layer, whose report is not committed. This receipt records only the generic wording changes. It does not include question text, reader outputs, scores or expected-answer content, and it does not add any claim, pin or runtime result.

## Changes

- **[SOURCE_FRESHNESS.md](../SOURCE_FRESHNESS.md)** gained one section, `Commit identity and selected blobs`, before the worked check. It states that the phrase “same commit as pin” requires equal commit identity. It separates that from unchanged selected blobs at a different commit, which support only a named-scope result. It requires comparisons to be grouped by repository against that repository's own accepted pin. It includes one example, labeled hypothetical, of a different commit with unchanged selected paths and of a changed path in one repository.
- **[START_HERE.md](../../START_HERE.md)** gained one step, `4`, in its How to continue list. It asks each task answer to name the applicable source commit or commits for every repository used, the platform and configuration, and any authorization, eligibility and identity-phase premise that a prospective execution needs. It links the existing continuation prompt, which already requests these fields, and states that an unsupplied field is UNKNOWN rather than an inferred pin.

The four freshness states, the accepted pins, the worked RC-0012/0013 same-commit result, the original ref receipt in that worked check, the continuation prompt, the claims, the knowledge dossiers, the frontiers and every frozen report are unchanged.

## Checks

- `git diff --check` is clean. The diff inserts 12 lines and deletes none, in the two changed files.
- Relative Markdown links and anchors in the two changed files resolve, including the continuation-prompt anchor.
- The changed paths relative to r3 are `START_HERE.md`, `docs/SOURCE_FRESHNESS.md` and this receipt. All other tracked files are byte-identical to r3.
- No live ref query, source audit, runtime, upstream execution, reader rerun, push or external write was performed. No reader answer, expected-answer content or protocol file was read or integrated.

## Limits

This change clarifies how a reader should state applicability. It does not validate any reader answer, establish that the navigation now succeeds for the reader, or qualify any new source branch. The same-reviewer source recheck covers both the freshness and navigation text. Any later reader repair check and parent integration remain separate steps.

Model billing, token totals and elapsed duration are unknown, so this receipt makes no cost, speed or usability claim.
