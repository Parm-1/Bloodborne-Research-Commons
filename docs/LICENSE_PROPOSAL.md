# Documentation license — ADOPTED: CC BY 4.0 (proposal and adoption record)

Status (2026-10-12): **adopted** by the owner's explicit approval, relayed by the project parent. The unmodified official legal code is the [LICENSE](../LICENSE) file. The text below is the original proposal, retained, with the adoption record at the end. No rights audit was performed beyond the owner's approval; this is not a legal opinion. The repository is published (see [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md)).

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

## Attribution wording

> Bloodborne Research Commons, Parm-1 and contributors, licensed under CC BY 4.0.

## Owner confirmations (as proposed; resolved in the adoption record)

1. The owner has, or can grant, the rights to license the original prose. A license cannot add rights the licensor does not hold; the owner should decide whether anything in the text needs further provenance (for example any AI-assisted drafting) before granting.
2. Whether inbound contributions are accepted under the same license (a pull-request checkbox is the simplest mechanism) or under a different arrangement.
3. Whether CC BY 4.0 is preferred over a more permissive dedication or a different license. Attribution is the reason it is proposed: it keeps citations traceable.

## Dependency and attribution caveats

- This repository copies no upstream source or assets. It links to files at pinned commits and paraphrases them; identifiers such as function and field names are cited for reference.
- Upstream projects keep their own licenses ([declared licenses and evidence](SOURCE_REVIEW.md#license-statements-found)): bbhost GPL-3.0-or-later; bbport and shadPS4 GPL-2.0-or-later, with bundled third-party components under other licenses. CC BY 4.0 on this repository's prose does not relicense, clear or interpret any of them.
- This review makes no determination about combining code from these projects. Do not import, combine or redistribute upstream code on the strength of this repository; any such use needs a per-file review of the exact upstream licenses first, and that review has not been done.
- Future original utilities need a separate license decision; if they derive from a GPL project they must follow that project's terms.
- Attribution to upstream authors is preserved through links and the pinned source register. No endorsement or affiliation is implied.

## Adoption record (2026-10-12)

- **LICENSE:** the official plain-text legal code fetched over HTTPS from <https://creativecommons.org/licenses/by/4.0/legalcode.txt>, stored byte for byte (18,657 bytes, SHA-256 `9ba9550ad48438d0836ddab3da480b3b69ffa0aac7b7878b5a0039e7ab429411`; the same size as the copy read for the proposal).
- **Scope:** as proposed above (Markdown documents, `llms.txt`, the pull-request template, and the original wording and structure of `sources/projects.yaml`). The preserved review reports under `docs/reviews/` are repository documentation written for this project and unchanged; the owner's approval covers the repository's original documentation, and the upstream material they quote or link stays under its own licenses.
- **Confirmations:** the owner approved CC BY 4.0 for original documentation (confirmation 1 and 3), and inbound contributions under the same license (confirmation 2).
- **Notices added:** README, CONTRIBUTING (inbound-license statement) and a pull-request template checkbox.
- **Unchanged:** upstream licenses, the dependency caveats above and the no-determination statement on combining upstream code.
