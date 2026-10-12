# Start here

## Readers

1. Define the exact task (e.g. GX resource lifetime; differential test of one game function; shader translation).
2. Consult [sources/projects.yaml](sources/projects.yaml) for the versioned projects.
3. Read the relevant claim in [claims/](claims/) and its cited upstream sources. Check the evidence level, exclusions, and date.
4. Consult [frontiers/](frontiers/) for open questions, distinguish confirmed facts from hypotheses, and review relevant upstream updates.
5. Continue in the *appropriate project*, with its own actual working tree, authority, assets, and acceptance rules. This public knowledge base is not an execution controller.

## Automated agents

Begin with [AGENTS.md](AGENTS.md) and [docs/CONTINUATION.md](docs/CONTINUATION.md). Use the smallest relevant source subset, not the entire corpus. Do not hallucinate an implementation or infer undocumented runtime observations from code. Respect project licensing and artifact restrictions.

## Starter evidence

The starter records describe public artifacts that were SOURCE_INSPECTED or PROJECT_REPORTED on 2026-10-12, and were checked against the pinned commits as recorded in [docs/SOURCE_REVIEW.md](docs/SOURCE_REVIEW.md). They **do not claim independently reproduced gameplay results**, and the independent source and documentation review of the first candidate ([review](docs/reviews/REVIEW-r1.md)) is not a game or runtime qualification; its findings were repaired and rechecked ([recheck](docs/reviews/REVIEW-r2.md)). The source register pins the exact upstream commits.

For the subsequent GX lifecycle investigation, read the [implementation dossier](knowledge/gx-resource-lifecycle.md). Its review status is separate from the starter review above.

For texture preparation, continue with the [focused source-lifetime dossier](knowledge/texture-prep-source-lifetime.md): separate CPU staging, hash-only completion, GPU reads and the original texture-owner ordering still unknown. Its [independent source review](docs/reviews/BRC-PREP-OWNERSHIP-01-REVIEW-r1.md) is complete and parent-accepted at source/documentation scope; fresh-reader validation remains pending at candidate r2.
