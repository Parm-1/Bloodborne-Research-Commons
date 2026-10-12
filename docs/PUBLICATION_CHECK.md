# Publication checklist

Status (2026-10-12): **PUBLISHED AND VERIFIED.** The owner-approved public repository is [Parm-1/Bloodborne-Research-Commons](https://github.com/Parm-1/Bloodborne-Research-Commons). The first publication was read back against the licensed commit and its complete file tree; the details below preserve the distinction between publication and technical review. Original documentation is licensed under CC BY 4.0 ([LICENSE](../LICENSE)).

Before making the first public commit or enabling external contributions:

- [x] Confirm repository ownership/name, visibility, and who can write or administer it. *Decided; see below. Name availability is confirmed only when the hosted repository is created.*
- [x] Approve a clear license for original documentation. Do not auto-relicense upstream material. *CC BY 4.0 adopted; see [LICENSE_PROPOSAL.md](LICENSE_PROPOSAL.md#adoption-record-2026-10-12).*
- [x] Review every included file for game bytes/assets, personal/private records, credentials, unapproved captures and unpublished third-party material. *Author static scan and the independent review of candidate-r1 found none; see [SOURCE_REVIEW.md](SOURCE_REVIEW.md) and [REVIEW-r1](reviews/REVIEW-r1.md).*
- [x] Check that citations resolve to pinned public commits. Confirm claims are scoped and do not fabricate runtime validation. *Author check done; the independent review of candidate-r1 raised five findings, all repaired in candidate-r2 and confirmed by the same reviewer's recheck ([REVIEW-r2](reviews/REVIEW-r2.md)).*
- [x] Preserve upstream authorship and trademark/non-affiliation statements. *README and source register carry them.*
- [x] Ensure no BBPC internal private paths, operational authority or source patches are imported by default. *Static scan and review passed.*
- [x] Demonstrate a fresh-agent cold-start read on a specific question; review its unsupported claims before release. *Completed by an uninvolved reviewer on candidate-r1 ([answer in REVIEW-r1](reviews/REVIEW-r1.md#independent-cold-start-answer)); the corrections it required were made in candidate-r2 and confirmed by the recheck ([REVIEW-r2](reviews/REVIEW-r2.md)).*

## Technical completion (not an owner decision)

Routine technical acceptance belongs to the project's parent integrator, not to the first-publication owner decision below. It is done: the same reviewer rechecked the five findings, the license-caution change and the status statements ([REVIEW-r2](reviews/REVIEW-r2.md)), and the integrator accepted candidate-r2 at bounded public-source and documentation scope. That scope is not a game, fixture or runtime qualification, a legal conclusion or a rights assessment.

## Final integration record

Candidate-r3 (2026-10-12) is the mechanical integration of that acceptance: the unchanged recheck report added as `reviews/REVIEW-r2.md`, review-status lines changed from pending to completed, and one leftover template fragment in RC-0001's r2 note replaced by its link. Claim bodies, levels, source pins and exclusions are unchanged; the only edit to an earlier revision note is the named replacement of the leftover template fragment in RC-0001's r2 note. Checks were limited to the changed prose and local links; the full source, hash and URL inventory was not repeated (see the r3 note in [SOURCE_REVIEW.md](SOURCE_REVIEW.md#revision-notes)). Candidates r1 and r2 and the seed are preserved by Git tags.

Local checks run for r3: 18 tracked text files decode as UTF-8 with no BOM, NUL or carriage return; 80 relative Markdown links and anchors resolve; a scan for private paths, credential prefixes and e-mail addresses found 0 hits. The template fragment now appears only inside the unchanged recheck report, which quotes it. Carried unchanged from the candidate-r2 record, not rerun: the 13 source-file hashes, 35 pinned and 40 distinct URLs reachable, the limited YAML line-shape check (no YAML parser was used), and the seed-original inventory of 14 files and 20,099 bytes.

Candidate-r4 (2026-10-12) corrects two bookkeeping statements in r3 without changing any claim body, level, pin, exclusion or report: RC-0001's r3 note wrongly said its review-status line had been updated (that line is unchanged from r2), and the statement above about earlier revision notes ignored the named RC-0001 correction. It also clarifies that "no repository has been created" means no hosted repository. Reports, tags and the 80-link and source-inventory checks of r3 are carried unchanged; no check was rerun.

## First-publication decision (owner) — decided 2026-10-12

The owner explicitly approved the following, relayed by the project parent. These are the recorded decisions; the hosted repository was created and verified as recorded below.

1. **Owner and repository name.** `Parm-1/Bloodborne-Research-Commons`. The repository was created under this owner and name.
2. **Visibility.** Public. This publishes the whole Git history.
3. **Documentation license.** CC BY 4.0 for original documentation, with the official unmodified legal code as [LICENSE](../LICENSE) ([adoption record](LICENSE_PROPOSAL.md#adoption-record-2026-10-12)).
4. **Contribution intake.** The owner is sole administrator; issues and pull requests are enabled; contributions are accepted under the same license ([CONTRIBUTING.md](../CONTRIBUTING.md)).
5. **Git author identity.** New commits use the owner's GitHub no-reply identity (repository-local Git configuration). Older commits (the seed and candidates r1 to r4) keep the neutral placeholder author. They are not rewritten, because the frozen review reports, tags and recorded hashes cite those exact commits; rewriting would break that evidence. The placeholder carries no personal address.

**Publication state:** published and verified. The parent created the hosted repository, pushed the licensed commit and preserved tags, and read them back through GitHub.

## Release-preparation record

The licensed release candidate is the commit tagged `licensed-release-r1`, the successor of candidate-r4 (`2090f57cdd611a62d8a124aa1bdb81fc2d1d5ee5`). It adds the LICENSE file, the notices above and the decision records. Claim bodies, evidence levels, source pins, exclusions and the frozen reports are unchanged. The earlier "pending owner decision" wording in this file, the README, CONTRIBUTING and `llms.txt` was replaced by the decisions above. Static checks for this commit and the release archive are in [SOURCE_REVIEW.md](SOURCE_REVIEW.md#revision-notes); the source, hash and URL inventory from r2 and r3 is carried unchanged and was not refetched.

## Not required for the first release

Licensing of future original utilities, and the per-file license review that any future import of upstream code would need. Neither applies while the repository contains documentation only.

No code, scripts that execute upstream code, game data, private project state or account details are in the candidate. Upstream maintainers have not been contacted.

## Verified first publication (2026-10-12)

- Initial published commit: `8411dc4c31d4b253302e7122465d9877660c2197`; tree: `55af5832c2803403e3e41c19790e6632d08612af`. GitHub returned those exact identities for `main`.
- Complete GitHub tree: all 19 file paths and Git blob identities matched the local licensed commit; no truncated response.
- Six preserved tags (`seed-original`, candidates r1 to r4, and `licensed-release-r1`) matched their local commit identities. Frozen review reports and source-claim bodies remain unchanged.
- GitHub repository settings: public, default branch `main`, issues enabled. Collaborator readback listed only `Parm-1`, with role `admin`; pull requests remain available. No additional collaborator was granted access.
- Publication bookkeeping replaces the previously accurate pending status. The final documentation snapshot and archive use the linked `published-r1` tag; the licensed release candidate and its archive remain preserved. Publication is not evidence of gameplay, source execution, or legal review.
