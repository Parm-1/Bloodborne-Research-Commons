# Publication checklist

Status (2026-10-12, candidate-r2): **unpublished candidate.** Nothing has been published, no remote exists, no repository has been created and no license has been granted. Public visibility and code-license permission are separate decisions.

Before making the first public commit or enabling external contributions:

- [ ] Confirm repository ownership/name, visibility, and who can write or administer it. *Owner decision; see below.*
- [ ] Approve a clear license for original documentation. Do not auto-relicense upstream material. *Owner decision; CC BY 4.0 is drafted in [LICENSE_PROPOSAL.md](LICENSE_PROPOSAL.md), not adopted.*
- [x] Review every included file for game bytes/assets, personal/private records, credentials, unapproved captures and unpublished third-party material. *Author static scan and the independent review of candidate-r1 found none; see [SOURCE_REVIEW.md](SOURCE_REVIEW.md) and [REVIEW-r1](reviews/REVIEW-r1.md).*
- [x] Check that citations resolve to pinned public commits. Confirm claims are scoped and do not fabricate runtime validation. *Author check done; the independent review of candidate-r1 raised five findings, all repaired in candidate-r2; recheck pending.*
- [x] Preserve upstream authorship and trademark/non-affiliation statements. *README and source register carry them.*
- [x] Ensure no BBPC internal private paths, operational authority or source patches are imported by default. *Static scan and review passed.*
- [x] Demonstrate a fresh-agent cold-start read on a specific question; review its unsupported claims before release. *Completed by an uninvolved reviewer on candidate-r1 ([answer in REVIEW-r1](reviews/REVIEW-r1.md#independent-cold-start-answer)); the corrections it required are made in candidate-r2 and await the same reviewer's recheck.*

## Technical completion (not an owner decision)

Routine technical acceptance belongs to the project's parent integrator, not to the first-publication owner decision below.

1. The same reviewer rechecks the five findings, the license-caution change and the consistency of the status statements in candidate-r2.
2. The integrator records the review status in a final bounded commit and refreshes the pins.

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
