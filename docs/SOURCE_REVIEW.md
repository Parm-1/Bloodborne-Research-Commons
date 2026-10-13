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

### Differential linked r2 — 2026-10-12

[Independent r1 review](reviews/BRC-DIFFERENTIAL-VALIDATION-01-REVIEW-r1.md) is integrated verbatim and hash-checked. Its F1 prospective-control prerequisite is repaired in the matrix/control, RC-0009 and frontier: non-sentinel pre-arm +0x14 and original-arm consumption evidence are required; already-sentinel omission is non-discriminating. Principal source findings, the 20 source pins and original static receipts are reused unchanged. [Author r2 repair receipt](reviews/BRC-DIFFERENTIAL-VALIDATION-01-AUTHOR-r2.md) records affected static validation; same-reviewer recheck and separate reader work remain pending.

### Differential integration r3 — 2026-10-12

[Same-reviewer affected r2 recheck](reviews/BRC-DIFFERENTIAL-VALIDATION-01-REVIEW-r2.md) is copied verbatim, SHA-256 `7596a3ef10a343cf767ea42efd949a0ced978dc82eb9208a796ec44f279ff019`. F1 is resolved with no remaining actionable finding in affected scope; parent accepted the repaired source/documentation contract. [Author r3 receipt](reviews/BRC-DIFFERENTIAL-VALIDATION-01-AUTHOR-r3.md) records mechanical status/report integration with technical bodies, controls, source identities and prior reports preserved. Earlier inspection/static receipts retain their exact scopes. Fresh-reader validation is pending; no execution evidence or authority is added.

### Differential final integration r4 — 2026-10-12

[Public-only fresh-reader report](reviews/BRC-DIFFERENTIAL-VALIDATION-01-FRESH-READER-r1.md), bound to PR 6 head `097fee0f7a2df451d7cddd1a4499eaf727564e5a`, is copied verbatim, SHA-256 `0ddf10b5ecf349b89ca1cc61a5aea96769bec11b9ff52b8068fea261b558ca99`. Parent accepted the reading result: no material navigation or unsupported-inference finding; summaries retain the reviewed NaN exceptions versus raw GSM. [Author r4 receipt](reviews/BRC-DIFFERENTIAL-VALIDATION-01-AUTHOR-r4.md) records focused final status/report checks and unchanged technical bodies, controls, source rows and prior reports. Source review, affected recheck and fresh-reader work are complete at their stated scopes; no execution claim or authority is added.

## Function correspondence extension — 2026-10-12

[BRC-FUNCTION-CORRESPONDENCE-01 guide](../knowledge/function-address-correspondence.md) traces two pinned public producers and one additional consumer; [RC-0012](../claims/RC-0012-address-coordinates.md), [RC-0013](../claims/RC-0013-unwind-provenance.md) and an append-only RC-0003 extension add coordinate/extent/output interpretation. Eight file identities and exact selected bounds are in the guide. [Author r1](reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r1.md) records focused identity/location/link/preservation/arithmetic checks; independent source review and fresh-reader work pending. Existing source/license ownership decisions and closed dossiers/reports remain unchanged. No tool, executable, fixture, native/game/GPU execution, private input or code import occurs; original hypothetical metadata does not qualify the upstream parser or a game graph.

## Function correspondence linked integration r2 — 2026-10-12

The [independent r1 source review](reviews/BRC-FUNCTION-CORRESPONDENCE-01-REVIEW-r1.md), SHA-256 `8ed8721985cfa77dd331c181e7be7f654bdd6104ca1f74aa6ec93b61bf886109`, is integrated verbatim: no actionable finding; parent accepted the source/documentation contract. [Author r2 receipt](reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r2.md) records focused mechanical checks. Entire prior prefix, technical findings/examples/contract, source identities and all frozen reports are preserved. Fresh-reader validation remains pending; no execution claim or authority is added.

## Function correspondence final integration r3 — 2026-10-12

The [public reader r1](reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r1.md) at PR 8 head `790ff6608cae66f8e73519932b51e4b7282c06e0` and [linked reader r2](reviews/BRC-FUNCTION-CORRESPONDENCE-01-FRESH-READER-r2.md) are integrated verbatim, SHA-256 `f12ec0e1c58251993f015846cf336ea7cdf401f5b85f9f1b92ccf81a7baec499` / `2197184cf6309b53bd36cc0e6cc00953c68d42d5e8865aa35e7c6e2c0fb1cd19`. Parent accepted the reading result with its wording qualification: only N−5 is a valid complete five-byte start omitted; N−4 through N−1 cannot fit one. Guide/RC-0003 were already correct; no technical repair. [Author r3 receipt](reviews/BRC-FUNCTION-CORRESPONDENCE-01-AUTHOR-r3.md) records final focused status/report checks. Source review and reader work are complete at their separate stated scopes; entire prior prefix, technical content, source identities and frozen reports remain unchanged. No execution claim or authority is added.

## Entry-layer review history, 2026-10-13

[Independent source and editorial review r1](reviews/BRC-AGENT-ENTRY-01-REVIEW-r1.md), SHA-256 `fe4ec0c48035c779f6f4d35ed3dcb6cc9ba2a1fd1456f42e3da18a015bb47046`, is copied verbatim. Its finding F1, that the address route required a runtime load base for every join, and its evidence-precision item R1 led to [candidate r2](reviews/BRC-AGENT-ENTRY-01-AUTHOR-r2.md). The [affected recheck r2](reviews/BRC-AGENT-ENTRY-01-REVIEW-r2.md), SHA-256 `75f1202a77891dc271d2d81fa3a6e6936e7ce62aa03853387614fc8f775f5006`, is copied verbatim and reports no remaining actionable finding in affected scope. [Author r3 receipt](reviews/BRC-AGENT-ENTRY-01-AUTHOR-r3.md) records this integration. The cross-topic fresh-reader usability result is pending. The entry layer adds no runtime, game, native or GPU claim.

## Entry-layer final integration, 2026-10-13

The frozen records of the entry-stage usability check are copied verbatim into `docs/reviews`. Each source hash was checked before copying, and each copy was checked byte-for-byte against its source.

| Record | SHA-256 |
|---|---|
| [Source recheck r4](reviews/BRC-AGENT-ENTRY-01-REVIEW-r4.md) | `fb4db6b1954ca98791544e425da2514715d6e61d4e459b91407e68503e6d01de` |
| [Usability protocol r1](reviews/BRC-AGENT-ENTRY-01-USABILITY-PROTOCOL-r1.md) | `0863c3ae933ef0911bc6592347946676408c73cd8eceb6ea6370cf9ebd16bbef` |
| [Usability questions r1](reviews/BRC-AGENT-ENTRY-01-USABILITY-QUESTIONS-r1.txt) | `cdce023fe73f3d74b551e014aa3493d4b785096c94ddf76c8b5a5daaecb554aa` |
| [Fresh reader r1](reviews/BRC-AGENT-ENTRY-01-FRESH-AGENT-r1.md) | `937e14eeaecdd1071ccdd2bb211307c8af6705cf587685aa0efcad28e5aa9479` |
| [Fresh reader r2](reviews/BRC-AGENT-ENTRY-01-FRESH-AGENT-r2.md) | `8352cb54950e6ed21d1a19c1e20c8b1942dade449936fc41f9854c7a87747283` |
| [Fresh reader r3](reviews/BRC-AGENT-ENTRY-01-FRESH-AGENT-r3.md) | `8faa6fc581de8b116d60643aa0f957e7e95412b4bd8e5042576cd9dc0cb77bb0` |
| [Usability assessment r1](reviews/BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r1.md) | `b46d37f24345e5e5cc9d49141c0de2cc05f2712dcae7540bc704052c2bcdc8b4` |
| [Usability assessment r2](reviews/BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r2.md) | `9e74400bdf64272c2f6643f13e90f1c070717c55013ee4cd4dcaba14c2852998` |
| [Usability assessment r3](reviews/BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r3.md) | `f2fecc2229bfb93a6484a2d75d292fc9f540404c5f6b3d0a1edbc755fb311495` |

The entry is accepted as a source-and-documentation entry at its reviewed scope. The source-review pull request decision is pending a Research Director editorial decision. The fixed whole usability criterion is not met. The original reading and each same-reader repair stage are kept separate, and the transport-corrected check permitted public continuation and validation contracts to be read without changing the criterion. The reviewer found no remaining source or entry defect. Reader retries have stopped.

The pending wording in the entry-layer history above is historical. This section and [CORPUS_CHECKPOINT.md](CORPUS_CHECKPOINT.md#current-entry-status-brc-agent-entry-01-2026-10-13) supersede it. The Question 2 reasoning failure and the Question 3 partials are reader reasoning findings, not new source claims. Accepted technical claims, dossiers, frontiers and the source registry are unchanged.

## Entry-layer continuation r6, 2026-10-13

PR #10 received an owner review with partial editorial acceptance. The task-first documentation and the preserved negative reading result are supported at source and documentation scope. The adequate-usability gate is not accepted ([owner review](https://github.com/Parm-1/Bloodborne-Research-Commons/pull/10#pullrequestreview-5497980388)). This continuation adds the overlapping-reader explanation and the premise-labelling rule to [CONTINUATION.md](CONTINUATION.md#texture-upload-readers-that-overlap). It updates the [current status](CORPUS_CHECKPOINT.md#current-entry-status-brc-agent-entry-01-2026-10-13), and it adds one non-affiliation sentence to the README boundaries. The frozen usability records and all earlier grades are unchanged. A prospective evaluation design is a separate later candidate and is neither commissioned nor executed here.

## Entry publication closeout — 2026-10-13

[BRC-PRO-20261012-012](https://github.com/Parm-1/Bloodborne-Research-Commons/pull/10#pullrequestreview-5498555564) accepts the documentation and preserved negative evaluation for documentation-only incorporation. PR #10 merged at `30a4a4b2d4e2285ddea1745ddb80d89ab0c7791d`, tree `ab73bd4bf3eac6e378ac205c7a4ded31d2f4228a`, identical to delivered packet `900bd44e5a8e30c9cefc8126a62b8ad84d66154c`. The separately commissioned USABILITY-02 attempt evaluated `4dcb72ff2531d116fec68986eff03fb75150cca3`, tree `5946a03af18354781ad0b2a0c497cbee2a01c128`; its [original answer](reviews/BRC-AGENT-ENTRY-USABILITY-02-ANSWER-r1.md), [observation record](reviews/BRC-AGENT-ENTRY-USABILITY-02-OBSERVATIONS-r1.md), [independent grades](reviews/BRC-AGENT-ENTRY-USABILITY-02-GRADES-r1.md) and [result](reviews/BRC-AGENT-ENTRY-USABILITY-02-RESULT-r1.md) remain unchanged. The [historical assessment](reviews/BRC-AGENT-ENTRY-01-USABILITY-REVIEW-r3.md) remains unchanged too. Both whole usability criteria are NOT MET, and Issue #9 stays open.

This successor updates only current publication/status links in README, START_HERE and CORPUS_CHECKPOINT, and appends this history. Earlier dated pending/uncommissioned statements describe their original stages and are superseded for current status by this section and the checkpoint. Technical claims, evaluated versions, original answers, keys, grades, source pins and prospective designs are preserved. Source review does not establish reliable autonomous continuation: task relevance, evidence scope and consequential conclusions still need checking against cited producers/consumers. No reader retry, source survey, model change, new research topic or execution is part of this closeout.

[Independent affected review](reviews/BRC-AGENT-ENTRY-PUBLICATION-CLOSEOUT-01-REVIEW-r2.md), SHA256 `efe060da2e26a51dcd3b6e7a987f6a6009552a021ac0cadd77e3a31e078764e2`, found no actionable finding in the four-file status candidate `0ccd27ecad1c1dc3bbe636e398f1d3626eeb4755`, tree `eb1fa2794e97bdca67eb50a5eab797e20883b515`. It independently checked publication/evaluation identities, both negative-result links, 85 unchanged files, the historical source-review prefix, the technical checkpoint table, 125 relative references and 10 anchors. Final integration adds only that verbatim public-safe report and this citation; it does not rerun or regrade either usability check.

## Proposed cache applicability inspection — 2026-10-13

BRC-CACHE-APPLICABILITY-01 extends only bbport cache inspection at existing registry commit `3c57da4198ad62039f63f33bfd205b9916518acf`, verified tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. The [dossier](../knowledge/shader-pipeline-cache-applicability.md#source-identity-and-inspected-bounds) records 20 whole-file blob identities and exact selected text bounds: actual program-value producer, directional specialization and compilation consumer, render key/pipeline path, profile construction, explicit replacement and renderer persistence. Existing top-level freshness date, pins, license fields and earlier source-review prefix are preserved.

The [author r1](reviews/BRC-CACHE-APPLICABILITY-01-AUTHOR-r1.md) records source/static/hypothetical reasoning checks and resource closure. Independent source review remains pending; the author does not approve the contract. Original source-faithful controls are not upstream, serialized, native-fixture or game execution. No public source code is imported; selected SPDX and provenance inspection is reference-only and grants no code-combination authority. Proposed claims RC-0016/RC-0017 do not change accepted topics or Issue #9's OPEN / NOT MET result.
