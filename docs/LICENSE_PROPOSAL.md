# Documentation license proposal — DRAFT, not in effect

Status: proposal for the owner's decision. This repository currently has no license grant. Nothing in this file licenses anything. The owner must approve the license and confirm the rights described below before any LICENSE file or license notice is added (see [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md)).

## Proposal

License the original documentation prose under **Creative Commons Attribution 4.0 International (CC BY 4.0)**: <https://creativecommons.org/licenses/by/4.0/> (legal code: <https://creativecommons.org/licenses/by/4.0/legalcode>).

Covered, if adopted: the Markdown documents, `llms.txt`, the pull-request template, and the original wording and structure of `sources/projects.yaml`.

Not covered: third-party projects, code, names, logos and trademarks; the linked upstream sources; Bloodborne, its trademarks, binaries and assets, none of which are included here.

## What CC BY 4.0 does (from the official legal code, checked 2026-10-12)

- Anyone may reproduce, share and adapt the licensed material for any purpose, including commercial use (Section 2(a)).
- Users must give attribution, indicate whether they modified the material and link to the license (Section 3).
- The grant is worldwide, royalty-free, non-exclusive and irrevocable while the license terms are followed; it ends automatically for a user who breaches it, with reinstatement if cured (Section 6).
- Patent and trademark rights are not licensed, and moral rights are not licensed beyond the limited waiver in Section 2(b).
- Because the grant cannot be withdrawn for compliant users, adopting it is a lasting decision for the text published under it.

## Suggested attribution wording (owner to complete)

> Bloodborne Research Commons, <owner or project name>, licensed under CC BY 4.0.

## Owner confirmations needed before adoption

1. The owner has, or can grant, the rights to license the original prose. A license cannot add rights the licensor does not hold; the owner should decide whether anything in the text needs further provenance (for example any AI-assisted drafting) before granting.
2. Whether inbound contributions are accepted under the same license (a pull-request checkbox is the simplest mechanism) or under a different arrangement.
3. Whether CC BY 4.0 is preferred over a more permissive dedication or a different license. Attribution is the reason it is proposed: it keeps citations traceable.

## Dependency and attribution caveats

- This repository copies no upstream source or assets. It links to files at pinned commits and paraphrases them; identifiers such as function and field names are cited for reference.
- Upstream projects keep their own licenses ([declared licenses and evidence](SOURCE_REVIEW.md#license-statements-found)): bbhost GPL-3.0-or-later; bbport and shadPS4 GPL-2.0-or-later, with bundled third-party components under other licenses. CC BY 4.0 on this repository's prose does not relicense, clear or interpret any of them.
- GPL-3.0-or-later and GPL-2.0-or-later code is generally combinable only under GPL-3.0, and only where every component actually carries the "or later" grant, which has not been audited. This is a caution, not legal advice. Do not combine, import or redistribute upstream code on the strength of this repository.
- Future original utilities need a separate license decision; if they derive from a GPL project they must follow that project's terms.
- Attribution to upstream authors is preserved through links and the pinned source register. No endorsement or affiliation is implied.

## If the owner adopts it

1. Add the official CC BY 4.0 legal code as `LICENSE` (unmodified) and a one-line notice to the README.
2. Update [CONTRIBUTING.md](../CONTRIBUTING.md) and the pull-request template with the inbound-license statement.
3. Mark this file as adopted with the date, and update the decision record in [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md).
