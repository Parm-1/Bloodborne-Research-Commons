# Source review (author check, 2026-10-12)

Status (candidate-r4): checked by the author, then reviewed once by an uninvolved reviewer. The bounded source and documentation review of candidate-r1 (commit `c517ebd4758ddf1a920c50bda2e72dd580b7d0fa`) is preserved unchanged as [reviews/REVIEW-r1.md](reviews/REVIEW-r1.md). It independently fetched the 13 hashed files and confirmed the blob hashes, ran the cold-start exercise in [CONTINUATION.md](CONTINUATION.md), and raised five findings, all repaired in candidate-r2. The same reviewer's affected recheck of the repairs ([reviews/REVIEW-r2.md](reviews/REVIEW-r2.md)) found no remaining finding, and the integrator accepted candidate-r2 at this bounded public-source and documentation scope. This is not a game, fixture or runtime qualification, and not a legal or rights assessment.

## Method

For each pinned commit in [sources/projects.yaml](../sources/projects.yaml) the author confirmed that the commit resolves on the public upstream repository (commit date from the public GitHub commits API), fetched the cited files from `raw.githubusercontent.com` at that commit, read them in full, and recorded the git blob hash of each (the SHA-1 `git hash-object` gives for the fetched bytes). Nothing from the upstream repositories was cloned into, copied into or executed from this repository; the fetched files were saved only in a temporary directory outside this repository. No game, executable, fixture, paid API or upstream contact was involved.

## Claim results

| Claim | Result | Decisive lines at the pinned commit |
|---|---|---|
| [RC-0001](../claims/RC-0001-gx-resources.md) | Confirmed with scope corrections (r1) | [record fields](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L33-L45), [id is identity](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L12-L16), [write sequence](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L18-L22), [address lookups and overlap](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L54-L58), [unmap and protect](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L59-L66), [unseen objects get id 0](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/engine/gx_resources.h#L82-L84) |
| [RC-0002](../claims/RC-0002-decomp-compare.md) | Confirmed with scope corrections (r1) | [rule and two checks](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md#L9-L12), [SHA-256 gate](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md#L234-L237), [offline test](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md#L271-L281), [in-game compare](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md#L282-L289), [skip when no executable](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h#L1-L5), [executable load and guest state](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h#L7-L14), [same_float](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h#L105-L112) |
| [RC-0003](../claims/RC-0003-callgraph-limits.md) | Confirmed with scope corrections (r1); script read, not run | [docstring](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L2-L6), [segment and function table](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L10-L26), [byte scan](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L37-L49) |
| [Frontier](../frontiers/resource-ownership.md) | bbhost rendering bullet confirmed; bbport bullet reworded to what the README supports | [GX hooks](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/rendering.md#L20-L21), [bbport vs shadPS4 table](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/README.md#L94-L108) |

Seed statements that were corrected rather than confirmed: "registry generation" (no such field), "bbport cache UID" (not found in anything read), "CI skip" (CI is not in the cited sources), the bbport license evidence file path (`gpu/VENDOR.txt`, not a root file), and the registry's "upstream corrections" research use (not supported). See each claim's revision notes; the original text is the `seed-original` Git tag.

## Source blob hashes (git SHA-1 of the file bytes at the pinned commit)

| File | Blob |
|---|---|
| bbhost `src/engine/gx_resources.h` | `f6edcb582e141aabfa30384e381fb79f10e9653c` |
| bbhost `docs/decomp.md` | `3ce60ba7f09b1401631f9567dba26e1af028fa6b` |
| bbhost `tests/decomp/eboot_kit.h` | `3efca4382246527daa6d5d31f5a1d36b41ee1ec6` |
| bbhost `docs/rendering.md` | `c2f36e08ccdbd5251c59c86878c75b6edb2b97d0` |
| bbhost `README.md` / `LICENSE` | `dcf07c6aebd6bbfd5ef3c31884fa08d94bd0979c` / `94a9ed024d3859793618152ea559a168bbcbb5e2` |
| bbport `tools/re/callgraph.py` | `034c98b92e163f21a17163c7daf0393e7c7b89dc` |
| bbport `README.md` / `LICENSE` | `b7004d7901749ab08dd296ac4f198c230ca19dda` / `9efa6fbc962836e243e20f7f23db062e2c077d28` |
| bbport `gpu/VENDOR.txt` | `4a8603c7854cfb254ae105f8f21b34d36a6cf102` |
| shadPS4 `README.md` / `LICENSE` / `REUSE.toml` | `0161e2215a47822efb977fb8db5d8d22a090dcd0` / `d159169d1050894d3ea3b98e1c965c4058208fe1` / `9d1341c9ed0d4c70b515840dc1799d6986a0564e` |

## License statements found

These are what each project says about itself. They are not legal conclusions and grant nothing from this repository.

| Project | Declared | Evidence |
|---|---|---|
| bbhost | GPL-3.0-or-later | [README License section](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/README.md#L180-L190); [LICENSE](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/LICENSE) is the GPL version 3 text |
| bbport | GPL-2.0-or-later | [README Credits and licenses](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/README.md#L394-L398); [LICENSE](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/LICENSE) is the GPL version 2 text; [gpu/VENDOR.txt](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/VENDOR.txt#L1-L5) records vendored shadPS4 code (commit b4e7ae7, not the shadPS4 commit pinned here) |
| shadPS4 | GPL-2.0-or-later | README [SPDX header](https://github.com/shadps4-emu/shadPS4/blob/e0a466753a1aacbc8db8253be685bf7ab4d9daae/README.md#L1-L4) (GPL-2.0-or-later) and [License section](https://github.com/shadps4-emu/shadPS4/blob/e0a466753a1aacbc8db8253be685bf7ab4d9daae/README.md#L209-L211) (link labelled GPL-2.0), [LICENSE](https://github.com/shadps4-emu/shadPS4/blob/e0a466753a1aacbc8db8253be685bf7ab4d9daae/LICENSE) (GPL version 2 text) and [REUSE.toml](https://github.com/shadps4-emu/shadPS4/blob/e0a466753a1aacbc8db8253be685bf7ab4d9daae/REUSE.toml); REUSE.toml also lists BSL-1.0, MIT, BSD-3-Clause, OFL-1.1 and CC0-1.0 paths |

Not audited: per-file headers, `third_party/` and other bundled components, and the license of each individual file. This review draws no conclusion about combining code from the projects. Any future import of upstream code needs a per-file review first; see [LICENSE_PROPOSAL.md](LICENSE_PROPOSAL.md) for the dependency caveats.

## Not established

- No claim was run, reproduced or tested; nothing here is GAME_OBSERVED or OWNED_TESTED.
- RC-0001 inspected a header only; the registry implementation, hook coverage and any bbport equivalent were not read.
- RC-0002's zero-difference counts and RC-0003's behavior on a real executable are not reproduced.
- Upstream commits are snapshots; later upstream changes were not checked.

## Reproducing the source check

```sh
# For each pinned commit <commit> of repo <owner/name> and file <path> (HTTPS GET):
#   raw.githubusercontent.com/<owner/name>/<commit>/<path>   then: git hash-object <saved file>   (compare with the table above)
#   api.github.com/repos/<owner/name>/commits/<commit>        (commit exists; committer date)
```

## Static validation of this repository

The checks and results are in the validation record below.

### Validation record

Run for candidate-r2 on the working tree before its commit (2026-10-12), by a throwaway script kept outside the repository (the checks are listed so they can be repeated by any equivalent tool; no scaffolding is added here):

| Check | Result |
|---|---|
| Every non-`.git` file decodes as UTF-8, with no BOM, NUL byte or carriage return (a binary would fail) | 17 of 17 files pass |
| Every relative Markdown link resolves to an existing file, and every `#anchor` to an existing heading | 63 links pass |
| Every pinned `github.com/.../blob/<commit>/...` URL uses a commit registered in `sources/projects.yaml` for that repository, fetches successfully over HTTPS, and any line range lies within the file | 35 pinned URLs pass; 3 registered pins |
| Every other distinct URL (repository, license pages) returns success | 40 distinct URLs in total pass |
| Every 40-hex blob hash written in the documents equals the git blob hash of the fetched pinned file (or is a registered commit, a commit of this repository, or the vendored shadPS4 commit quoted from `gpu/VENDOR.txt`) | all pass |
| Pattern scan for absolute home or drive paths, tilde home paths, key or token prefixes, private-key headers, e-mail addresses, and common credential words | 0 hits |
| `sources/projects.yaml` shape (key: value lines; no value containing `: ` or ` #`) | limited line-shape check passes. PyYAML and Ruby are not installed and nothing was installed, so no YAML parser has read the file |
| Git history author and committer identities | neutral placeholder only |
| `seed-original` tag | 14 files, 20,099 bytes (the parent-reported size of the original archive) |

The candidate-r1 record had the same checks and outcome with 16 files, 51 links, 31 pinned URLs and 36 distinct URLs. A finding in any check blocks delivery. Limits: link checks show a page resolves, not that it still says the same; the blob-hash check establishes only the identity of the fetched bytes. That the cited text was read is the author's recorded inspection, which the independent reviewer repeated for the 13 hashed files.

## Revision notes

- **r2, 2026-10-12** (candidate-r2, successor to candidate-r1, commit `c517ebd4758ddf1a920c50bda2e72dd580b7d0fa`, which is preserved by its tag). Repairs from [reviews/REVIEW-r1.md](reviews/REVIEW-r1.md): finding 4, the blob-hash check is now described as establishing byte identity only, with reading attributed to the recorded inspection; finding 5, the shadPS4 SPDX header qualifier (GPL-2.0-or-later, README lines 1-4) is kept in the registry and the license table; the cross-project GPL combination sentence in the license proposal is replaced by a no-determination statement and the per-file caution; the status paragraph and validation record are updated. Findings 1 to 3 are repaired in the claims and in [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md). The earlier text is retained in the candidate-r1 Git version.
- **r3, 2026-10-12** (candidate-r3, final integration; predecessor candidate-r2 is preserved by its tag). Copied the recheck report unchanged to [reviews/REVIEW-r2.md](reviews/REVIEW-r2.md); replaced the recheck-pending statements with the completed bounded review; fixed the leftover template text in RC-0001's r2 note. No claim body, level, pin or exclusion changed. Checks for r3 covered only changed prose, local links and anchors (counts in [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md#final-integration-record)). The 13 source-file hashes, URL reachability (35 pinned and 40 distinct URLs) and the YAML line-shape check are carried from the candidate-r2 validation record above and were not rerun.
- **r4, 2026-10-12** (candidate-r4, bookkeeping only; candidate-r3 is preserved by its tag). Corrected RC-0001's r3 note to describe only what r3 changed, and corrected the final integration record in [PUBLICATION_CHECK.md](PUBLICATION_CHECK.md#final-integration-record). No claim body, level, pin, exclusion or review report changed.
- **release prep, 2026-10-12** (licensed release candidate, tag `licensed-release-r1`, successor of candidate-r4; r4 is preserved by its tag). Adopted CC BY 4.0 for original documentation and recorded the owner's publication decisions (details in the publication check and license adoption record). Claim bodies, levels, pins, exclusions and the frozen reports are unchanged. Local static checks for this commit, which also complete the r4 verification: 19 tracked files are UTF-8 with no BOM, NUL or carriage return; 87 relative Markdown links and anchors resolve; a scan for private paths, credential prefixes and e-mail addresses found 0 hits in the 18 non-LICENSE files and none in LICENSE. The 13 source-file hashes, URL reachability and the limited YAML line-shape check are carried unchanged from the candidate-r2 record and were not refetched. The official CC BY 4.0 text was fetched once to create LICENSE.

## Differential validation extension — 2026-10-12

The selected stateful follow-camera pair is traced through actual kit, loader/TLS, test, replacement, inline mouse/frame-rate helpers and build/CTest branches in the [dossier](../knowledge/original-code-differential-validation.md). Its inspected bounds and 20 decisive whole-file blob pins are listed there; selected inspection is distinguished from complete-body reading. New SOURCE_INSPECTED claims RC-0009 to RC-0011 and the appended RC-0002 qualification do not replace this document's historical checks, header-only scope or PROJECT_REPORTED counts. [Author r1](reviews/BRC-DIFFERENTIAL-VALIDATION-01-AUTHOR-r1.md) records focused static checks and closure. Independent review and fresh-reader validation are pending; no upstream tools, binary, fixture, native/game/GPU execution or code import was involved.
