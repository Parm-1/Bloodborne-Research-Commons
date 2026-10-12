# BRC-DIFFERENTIAL-VALIDATION-01 — author repair r2

Date: 2026-10-12. Linked successor to frozen candidate r1 `229e3158b10764c671580a90a1c6a8296d6b5297`, tree `57cd162ad693a1b53801abdd34e546adccda3b84`. Candidate tag: `brc-differential-validation-candidate-r2`. Exact successor commit/tree/dossier blob and report SHA-256 are returned after commit; this report avoids circular self-identity. Same original author retains candidate writer ownership; parent retains acceptance/publication.

## Finding and repair

[Independent r1 review](BRC-DIFFERENTIAL-VALIDATION-01-REVIEW-r1.md), SHA-256 `3ee97030ffa22e7551570a3dc6361eea916e98f155c8ed63a8209cc3b86372fd`, is integrated verbatim. Its one F1 is a missing prerequisite in the prospective omitted-override effect control. Public test lines 301–302 generate -1 with probability 0.9; replacement lines 536–549 write the consumed sentinel. If input already equals that sentinel, omission need not change raw post-state. This source-derived counterexample is not a `memcmp` defect or executed result.

The [dossier](../../knowledge/original-code-differential-validation.md) matrix, wrong-effect control and stop rule, [RC-0009](../../claims/RC-0009-camera-equality.md), and [frontier](../../frontiers/differential-validation.md) now require identical non-sentinel pre-arm +0x14 bytes plus original-arm post-consumption -1 evidence before omission is treated as a discriminating negative. Already-sentinel input is explicitly non-discriminating. The adjacent frontier equality sentence is clarified: two-NaN payload differences are accepted by the word relation and excluded from a payload-fidelity claim. This changes prospective-control applicability/wording, not the producer, comparator, source pin, execution authority or research question. Related discovery/source/claim status records link the completed review and pending affected recheck. RC-0002 receives a new append; its full r1 prefix is preserved.

## Affected checks and reused evidence

Focused documentation checks cover changed UTF-8 texts without BOM/NUL/CR, relative links/anchors, pinned citation paths/ranges, Git whitespace, exact repair write scope, bounded public-text path/credential-prefix scan and unchanged file preservation. The copied review matches its original hash. Dossier source-identity rows are byte-identical to r1, so its 20 source-blob receipts are reused, not remeasured. Original author r1 report, frozen prior reviews and closed GX/preparation records remain unchanged; no original inventory, upstream execution or network resurvey is repeated. No YAML change occurred in r2.

Final affected receipt: 11 changed/added texts; 90 relative links/anchors; 98 pinned source citation occurrences at 81 distinct locations; 20 unchanged source-identity rows reused; 32 unchanged r1 files plus the full RC-0002 r1 prefix preserved; integrated review hash/verbatim match. All focused checks pass with zero errors. Count categories describe documentation checks, never runtime controls, reached branches or trials.

## Closure and next consumer

All author commands finish before frozen delivery. No child, persistent shell handle, shared runtime resource or native/game/GPU/fixture process is created. Public upstream stays read-only and clean. No private/memory/other-chat evidence, binary acquisition, upstream script execution, source import, executable generation, implementation/framework/service, host/security/license change, spend, contact or external publication occurs. Available package token/cost and elapsed-time measurements are unavailable/unmeasured.

Same uninvolved reviewer is the next consumer for F1 and adjacent affected wording recheck; fresh-reader validation follows parent dispatch afterward. Review and acceptance are not self-approved. r1 is immutable; further corrections require linked r3–r6. No automatic runtime campaign follows.
