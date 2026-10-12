# Publication checklist

Status (2026-10-12, candidate-r4): **unpublished candidate.** Nothing has been published, no remote exists, no GitHub or other hosted repository has been created (only this local Git repository exists) and no license has been granted. Public visibility and code-license permission are separate decisions.

Before making the first public commit or enabling external contributions:

- [ ] Confirm repository ownership/name, visibility, and who can write or administer it. *Owner decision; see below.*
- [ ] Approve a clear license for original documentation. Do not auto-relicense upstream material. *Owner decision; CC BY 4.0 is drafted in [LICENSE_PROPOSAL.md](LICENSE_PROPOSAL.md), not adopted.*
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

## First-publication decision (owner)

This is the single home for the actions that remain reserved to the owner. Nothing below has been decided.

1. **Owner and repository name.** Proposed name: `Bloodborne-Research-Commons`. Availability under the chosen owner is not confirmed; a public 404 does not prove the name is free.
2. **Visibility.** Private until the other items are decided, or public. Making it public publishes the whole Git history.
3. **Documentation license.** Approve or change CC BY 4.0 and confirm the rights to license the original prose ([proposal](LICENSE_PROPOSAL.md)). Until then, no LICENSE file.
4. **Contribution intake.** Whether to enable issues and pull requests, who administers, and the inbound-license statement.
5. **Git author identity.** Local commits use a neutral placeholder author. The owner chooses the identity (for example a platform no-reply address) before the history is pushed, so a personal address is not published; changing it rewrites the history.

## Not required for the first release

Licensing of future original utilities, and the per-file license review that any future import of upstream code would need. Neither applies while the repository contains documentation only.

No code, scripts that execute upstream code, game data, private project state or account details are in the candidate. Upstream maintainers have not been contacted.
