# Bloodborne Research Commons independent affected recheck r2

Date: 2026-10-12. Exact candidate-r2: `4e737690757a33aff5c01190a47ea4156250b5b0`. Reviewed predecessor candidate-r1: `c517ebd4758ddf1a920c50bda2e72dd580b7d0fa`. Seed: `b73212910f135a12058c8c01b7b4dba00ceb80eb`.

Linked original review: [REVIEW-r1](REVIEW-r1.md), frozen SHA-256 `e7df5d6bb7dd8afaca16ac2b8118943b4681ecd8262605bcfdc9a76c49482a40`. This is the same uninvolved reviewer, rechecking the same author's repairs. No candidate file was written by the reviewer. This report is frozen on delivery; corrections require a linked successor.

## Result and repaired findings

Recommend bounded technical acceptance of candidate-r2, followed by the mechanical integration specified below. All five r1 findings are repaired, and the separately identified unsupported general GPL-combination statement is removed. There is no new substantive source/evidence defect requiring another repair/review cycle. Technical acceptance belongs to the parent integrator; the reviewer does not accept or publish for the owner.

1. RC-0002 now states both the upstream zero-difference world-session condition and the replacement performance-within-noise condition, citing the same pinned decomp document lines 287-289. This agrees with the raw source inspected during r1; the rule and results remain PROJECT_REPORTED, not reproduced.
2. RC-0003 now describes the actual `range(len(code) - 5)` bounds, offsets 0 through N-6, and explicitly identifies the omitted last possible five-byte start at N-5. The claim retains its instruction-boundary, FDE and indirect-edge exclusions. This agrees with the complete pinned scanner inspected during r1; no scanner was imported or executed.
3. PUBLICATION_CHECK separates parent-owned technical completion from reserved publication/license decisions. Future utilities and prospective code-import audits are explicitly outside first-release requirements. The checklist no longer adds human technical-review acceptance as a separate publication decision.
4. SOURCE_REVIEW now assigns the blob check to byte identity and assigns reading to the recorded inspection. It no longer treats the hash as proof of examination or semantic truth.
5. The registry and source-review license table distinguish the pinned shadPS4 README SPDX qualifier GPL-2.0-or-later from the License-section link labelled GPL-2.0. No per-file or combination-rights conclusion follows.

LICENSE_PROPOSAL substitutes a no-determination statement and per-file caution for the uncited cross-project combination conclusion. The documentation license remains a draft; no grant, rights audit or code import occurred.

## Affected status, links and identity

The entire r1-to-r2 delta was inspected: 11 changed files, comprising repaired prose, scoped review-status statements and the exact original report. README, START_HERE, CONTINUATION, SOURCE_REVIEW, PUBLICATION_CHECK and the affected claims consistently describe r1 review completion and r2 recheck pending. That pending status is accurate for the frozen pre-recheck candidate and is the subject of final mechanical integration, not a source blocker. The cold-start answer remains in the immutable r1 report; its phase, write/identity, consumer completion, positive and falsifier limits are unchanged. Independent source/documentation review does not promote header comments to implementation or game evidence.

The embedded `docs/reviews/REVIEW-r1.md` has exactly the commissioned SHA-256 and matches the original frozen report. Candidate-r1 and seed-original tags resolve to their commissioned commits. HEAD was the exact commissioned r2 commit and the working tree remained clean. The source blob-hash table is byte-identical to r1. Reused evidence: the 13 source-file bodies and hashes independently checked in r1; no complete upstream fetch/hash inventory was repeated.

Independent local-link verification found 63 relative Markdown file/heading links, all resolving, across 17 tracked files. The newly added external links target the same already inspected pinned sources and line ranges. The author's 35 pinned-URL and 40 total-URL validation counts were not independently reacquired during this affected recheck. The registry validation remains explicitly a limited line-shape check; no full YAML parse is claimed. Unchanged seed/content and public-text inventories are reused from r1; new prose and exact review inclusion introduce no private material or executable content found by this review. No external write or publication occurred.

## Mechanical final integration scope

The parent has commissioned same-author integration of this frozen recheck and a final technical-status commit. That work needs no further independent review if it stays within all of these conditions:

- Copy this report unchanged into `docs/reviews/REVIEW-r2.md`; verify its final SHA-256 against the delivered pin. Preserve REVIEW-r1 and both reviewed candidate commits.
- Add the report link and replace pending-recheck wording with the bounded completed-recheck result in existing documentation and claim review-status lines. Preserve primary evidence levels, technical claim bodies, source pins, exclusions and original revision history. Update existing validation counts only to actual measured results.
- Remove the literal `('+REV+')` template leftover in RC-0001's r2 revision note, replacing it with the existing REVIEW-r1 link. This is a mechanical citation cleanup, not a finding about the claim's semantics. Apart from this named note cleanup and review-status/link changes, the claim files must remain unchanged from r2.
- Keep unpublished/no-license status and reserved publication/license decisions intact. Do not add source code, new technical claims, runtime qualifications, a remote, publication or a license grant under this integration scope.

The parent should directly verify final report bytes, final commit identity, local links and this bounded diff. A substantive claim/source/authority change returns to the same repair/recheck loop; this recommendation does not grant that changed scope. No additional reviewer pass is needed for the mechanically checked integration above.

## Limits and closure

This is an affected source/documentation recheck, not new native-fixture, serialized-output, game or target-runtime evidence, and not a legal conclusion. The owner retains the reserved publication and documentation-license decisions. No runtime process, child, paid API or shared mutable resource was acquired; every read-only command completed and no live handle remains. Completion clock observed: 2026-10-12 07:33 UTC. Exact attributable token/cost usage and elapsed review duration were not measured and remain unknown.
