# BRC-AGENT-ENTRY-01 author receipt r2

**Scope:** successor repair of frozen candidate r1, `f14f2b257ad8e5d9fd888be403f82db479c0dc42`, tree `07e3af24fb3347b1f521f2958c39c1ead17e852d`, tag `brc-agent-entry-candidate-r1`. The accepted baseline is `74779fb1001ebbf82fc65fc399ab3ea44227c964`, tree `880e41e72a1994c1e62105cda6fce02cc4e5b43a`. The independent source and editorial review is a temporary report with SHA-256 `fe4ec0c48035c779f6f4d35ed3dcb6cc9ba2a1fd1456f42e3da18a015bb47046`; it is not a committed artifact. The r1 receipt and its tag are unchanged. This receipt is author evidence, not an independent review or a reader result.

## Repairs

- **Address route (review F1).** The README row required an actual runtime load base for every join. It now separates three premises: a same-image original-file point join needs established image identity, coordinate origins and an unambiguous, reversible segment mapping; a loaded-memory pointer also needs its loaded digest and actual slide; and an extent needs its own validated range premises. The wording follows the accepted [function-address guide](../../knowledge/function-address-correspondence.md) decision table and [RC-0012](../../claims/RC-0012-address-coordinates.md). The guide, claims, frontier and corpus checkpoint are unchanged.
- **Freshness record (review R1).** The r1 receipt and [SOURCE_FRESHNESS.md](../SOURCE_FRESHNESS.md) read as if the 2026-10-13T00:52:47Z clock came from the ref responses. It is a separate `date -u` value from the same parallel command batch. The returned commits are unchanged. The original commands and stdout are preserved verbatim below. No new ref query was made for this repair.

## Verbatim freshness observation

The parent session supplied these as the original single-read outputs, produced by the earlier author's tool calls. This successor did not have the earlier execution transcript and did not run a live query for this receipt.

Commands, launched in one parallel batch:

```text
/usr/bin/git ls-remote --symref https://github.com/deadinside28/bloodborne_pc.git HEAD
/usr/bin/git ls-remote --symref https://github.com/droogie/bbhost.git HEAD
date -u +%Y-%m-%dT%H:%M:%SZ
```

Stdout of the first command, with a tab between fields:

```text
ref: refs/heads/master	HEAD
3c57da4198ad62039f63f33bfd205b9916518acf	HEAD
```

Stdout of the second command, with a tab between fields:

```text
ref: refs/heads/master	HEAD
566184a74f071166299bb656c4af479e5bbe2771	HEAD
```

Stdout of the date command:

```text
2026-10-13T00:52:47Z
```

The date value is the batch clock for the three commands. Neither ls-remote response embeds a timestamp, so each ref response has no separate observation time in this record. Both returned commits equal the accepted registry pins for `bloodborne_pc` and `bbhost`.

## Changed paths and checks

Relative to frozen r1, this repair changes [README.md](../../README.md), [SOURCE_FRESHNESS.md](../SOURCE_FRESHNESS.md) and this receipt. Before freeze, I checked the local relative links and anchors in the three changed files, confirmed that the whitespace diff check is clean, and confirmed that the accepted claims, knowledge, frontiers, sources, AGENTS, evidence policy, the guide and corpus checkpoint are byte-identical to the r1 candidate. The earlier reports remain byte-identical to r1 and the baseline.

No unit test, runtime, upstream execution, reader work, YAML change or external write was performed. Model billing, token totals and elapsed duration are unknown, so this repair makes no cost or speed claim.
