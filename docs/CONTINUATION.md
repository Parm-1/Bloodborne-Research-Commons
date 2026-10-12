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
