# Bloodborne Research Commons

A community-oriented, evidence-qualified reference for Bloodborne PC porting, reverse engineering, decompilation, runtime compatibility, graphics, and verification.

**Status: unpublished candidate (2026-10-12).** Claims were checked against their pinned upstream commits by the author ([source review](docs/SOURCE_REVIEW.md)); an independent bounded review of candidate-r1 found five corrections, repaired in candidate-r2, and the same reviewer's recheck found no remaining finding ([review](docs/reviews/REVIEW-r1.md), [recheck](docs/reviews/REVIEW-r2.md)); no license is in effect. This is a research index, not a completed reverse engineering corpus or a shipping PC port. All technical claims are scoped to their cited versions and review level.

## The purpose

Connect public discoveries across projects so people and AI agents can answer: *What is known? How do we know? Which implementation already addresses this? What remains unproven?* The project aims to reduce duplicated investigations, not replace upstream repositories or repackage their code.

For first-time readers, open [START_HERE.md](START_HERE.md). For automated agents, read [AGENTS.md](AGENTS.md), then follow claim and source links. Contributions follow [CONTRIBUTING.md](CONTRIBUTING.md) and [Evidence policy](docs/EVIDENCE_POLICY.md).

## Initial research sources

- [bbhost](https://github.com/droogie/bbhost) — engine, GX resource knowledge, renderer work, comparative decompilation, tests and tools.
- [bbport](https://github.com/deadinside28/bloodborne_pc) — compatible game runtime, graphics translator, native-host work, and investigation tools.
- [shadPS4](https://github.com/shadps4-emu/shadPS4) — open-source PS4 system/graphics reference implementation.

Every source is linked to an exact research commit in [sources/projects.yaml](sources/projects.yaml), with the license statements found there. Upstream authorship and project licenses remain theirs. bbport's README states that it is not related to the shadPS4 project. No endorsement or affiliation with any project, Sony Interactive Entertainment or FromSoftware is implied.

## Important boundaries

- No copyrighted game executables, decrypted game binaries, proprietary assets, personal saves, protected captures, credentials, private research databases, or unapproved code imports.
- Public source comments and project reports are not game-validated truths; label them precisely.
- A documented interface is not proof that a natural Bloodborne consumer uses it.
- Availability of public code does not itself establish legal permission to combine or distribute derivatives. Validate the exact license and dependency graph.
- This repository does not grant authorization to run games, execute extracted code, alter private projects, contact researchers, or publish other people's work.

## Publication and licensing

This starter is unpublished until the owner decides to create and publish a repository. The decisions still pending (owner and repository name, visibility, documentation license, contribution intake) have one home: [docs/PUBLICATION_CHECK.md](docs/PUBLICATION_CHECK.md). The documentation license under consideration is CC BY 4.0, described in the draft [license proposal](docs/LICENSE_PROPOSAL.md); it is a proposal only and grants nothing until the owner adopts it. Third-party projects keep their own licenses; no external code is included.
