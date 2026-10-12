# Agent operating instructions

## Mission

Help people find existing, correctly scoped Bloodborne engineering knowledge, avoid reinvention, and design falsifiable next steps. Maintain citations and conservative claims.

## Mandatory working method

1. Establish the question and exact target version/platform. Read only the pertinent topic, claims, and upstream files.
2. Pin source identity: repo, commit, path, and, where useful, relevant line range and blob hash. A moving branch is a discovery source, not a stable proof.
3. Distinguish PROJECT_REPORTED, SOURCE_INSPECTED, OWNED_TESTED, GAME_OBSERVED, INDEPENDENTLY_REVIEWED, UNKNOWN, CONTRADICTED, and SUPERSEDED (definitions: [Evidence policy](docs/EVIDENCE_POLICY.md)). Do not collapse these into one VERIFIED boolean. Recording a reviewer is not a substitute for knowing its scope.
4. Describe the producing operation, data identity, consumers, lifetime, required outputs, and contradictory evidence. Reject claims whose required inputs are missing.
5. For reuse, determine ALREADY_PRESENT / USE_UNCHANGED / ADAPT / KNOWLEDGE_REFERENCE / DEFER / REJECT, and record licensing, ABI and dependency constraints.
6. Return one useful next step or an exact blocker. A broad survey is not a substitute for a consumer-backed proof.
7. Edit by proposed PR or issue with specific source references, changed claim IDs, and test plan. Do not silently promote uncertainty or rewrite history.

## Boundaries

This repo is public research only. Do not request or publish proprietary game binaries/data, personal saves, protected logs/screenshots, credentials or other people's private analysis. Do not execute game binaries or run tool scripts that mutate a host without authorization from the actual owner and project. Do not insert private BBPC state into this repository. Do not scrape private accounts or contact maintainers without consent.

If an external or source license is unclear, reference the idea and seek clarification rather than copying the code. When answering from this repo, cite exact origins and state known limitations.

Follow [docs/EVIDENCE_POLICY.md](docs/EVIDENCE_POLICY.md) and [docs/CONTINUATION.md](docs/CONTINUATION.md).
