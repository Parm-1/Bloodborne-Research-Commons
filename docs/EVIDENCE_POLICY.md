# Evidence and claim policy

A finding is useful only if it preserves **what was observed, where, how, and what it does not establish**.

## Levels

- **PROJECT_REPORTED**: upstream author's documentation or release claim; not reproduced here.
- **SOURCE_INSPECTED**: behavior of a specified source implementation or API description inspected at an exact commit. Does not prove runtime reachability. Statements in source comments about the game's own internals are the author's claims (PROJECT_REPORTED) unless corroborated.
- **OWNED_TESTED**: specified non-game fixture or synthetic data, with original test artifacts and meaningful falsifiers.
- **GAME_OBSERVED**: attributable execution in the actual game; must identify source, relevant state, timing/order, inputs, and limits. Does not automatically mean fidelity or generality.
- **INDEPENDENTLY_REVIEWED**: separate review occurred; its subject and scope must be identified alongside the primary level.
- **CONTRADICTED / SUPERSEDED / UNKNOWN**: preserve the negative or unresolved result instead of overwriting it.

## Minimum claim fields

Stable ID; atomic claim wording; subject/version/platform; evidence level; source URL pinned to commit/path; date checked; qualifying method; meaningful negative; exclusions and unresolved facts; upstream ownership/license; reviewer (if any); supersession link (if any).

A GitHub link is evidence of source publication, not of a game test. A hash binds bytes, not truth. A screenshot does not establish correct source input or lifetime. Repeated rows from one process are not independent trials. Likewise an identical result from related forks is not independent corroboration if it reuses the same implementation.

Do not report withheld or absent private tooling as intentional gatekeeping without evidence. Do not confuse absence from a public repository with absence of the author's private analyses.

## Changing a finding

Preserve the earlier claim and attach a dated revision/supersession note; do not retroactively rewrite unsupported historical claims into successes. Use matched controls and wrong-result tests where a tool can be executed lawfully. A stable public artifact should cite the original project rather than mirror code without a license review.

Git history is the preserved original. The seed commit is tagged `seed-original`; each corrected claim carries a dated revision note naming what changed and how to recover the earlier text.
