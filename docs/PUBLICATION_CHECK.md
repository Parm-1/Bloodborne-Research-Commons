# Publication checklist

Status (2026-10-12): **unpublished candidate.** Nothing has been published, no remote exists, no repository has been created and no license has been granted. Public visibility and code-license permission are separate decisions.

Before making the first public commit or enabling external contributions:

- [ ] Confirm repository ownership/name, visibility, and who can write or administer it. *Owner decision; see below.*
- [ ] Approve a clear license for original documentation; evaluate future code/tool licensing separately. Do not auto-relicense upstream material. *Owner decision; CC BY 4.0 is drafted in [LICENSE_PROPOSAL.md](LICENSE_PROPOSAL.md), not adopted.*
- [x] Review every included file for game bytes/assets, personal/private records, credentials, unapproved captures and unpublished third-party material. *Author static scan passed; see the validation record in [SOURCE_REVIEW.md](SOURCE_REVIEW.md).*
- [x] Check that citations resolve to pinned public commits. Confirm claims are scoped and do not fabricate runtime validation. *Author check done; independent review pending.*
- [x] Preserve upstream authorship and trademark/non-affiliation statements. *README and source register carry them.*
- [x] Ensure no BBPC internal private paths, operational authority or source patches are imported by default. *Static scan passed.*
- [ ] Demonstrate a fresh-agent cold-start read on a specific question; review its unsupported claims before release. *Pending: an uninvolved reviewer runs the exercise in [CONTINUATION.md](CONTINUATION.md).*

## First-publication decision (owner)

This is the single home for the actions that remain. Nothing below has been decided.

1. **Owner and repository name.** Proposed name: `Bloodborne-Research-Commons`. Availability under the chosen owner is not confirmed; a public 404 does not prove the name is free.
2. **Visibility.** Private until the other items are decided, or public. Making it public publishes the whole Git history.
3. **Documentation license.** Approve or change CC BY 4.0 and confirm the rights to license the original prose ([proposal](LICENSE_PROPOSAL.md)). Until then, no LICENSE file.
4. **Contribution intake.** Whether to enable issues and pull requests, who administers, and the inbound-license statement.
5. **Git author identity.** Local commits use a neutral placeholder author. The owner chooses the identity (for example a platform no-reply address) before the history is pushed, so a personal address is not published; changing it rewrites the history.
6. **Independent review result.** Accept or return the findings of the uninvolved review and cold-start exercise.
7. **Code licensing.** Only if original utilities are later added.

No code, scripts that execute upstream code, game data, private project state or account details are in the candidate. Upstream maintainers have not been contacted.
