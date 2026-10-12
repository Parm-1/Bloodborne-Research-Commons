# Continuation protocol for human and AI researchers

A fresh researcher must be able to continue without previous chat context.

1. **Question.** Name one precise engineering problem, target version/OS/GPU, and success criterion.
2. **Known state.** Cite exact claim IDs and upstream commits. State which claims are author-documented, source-inspected, tested, or unresolved.
3. **Reuse review.** Inspect the closest existing tool/implementation and assess the source/ABI/license/data dependencies. Explain if already present or unsuitable.
4. **Missing contract.** Identify the necessary producer, actual consumer, resource/source version, required sampling phase, lifetime, failure behavior or output.
5. **Smallest decisive experiment.** Freeze what outcome falsifies the proposal; prefer source and authorized owned-data controls. Do not assume access to game binaries or protected experiments.
6. **Return.** Document exact source, positive and negative evidence, limitations, decision, and one next action. A blocker must identify one missing fact/authority rather than say 'needs more RE'.

## First cold-start exercise

Without access to any private project or conversation, answer: "What does bbhost publicly document about game-owned GX resource identities and writes, and which specific game-reached observation would be needed before treating that as a safe-resource-lifetime contract in another port?" A successful answer cites pinned source, distinguishes header assertions from game evidence, and proposes one falsifier without manufacturing a game run.

## Status of the first exercise

An uninvolved reviewer ran this exercise from the public repository alone on candidate-r1. The answer and the review are preserved unchanged in [reviews/REVIEW-r1.md](reviews/REVIEW-r1.md#independent-cold-start-answer). The exercise is answerable without private material. It led to five corrections, made in candidate-r2; the reviewer's recheck of those corrections is pending. The exercise names a falsifier and an observation to gather; no game run was performed or is required for this repository.
