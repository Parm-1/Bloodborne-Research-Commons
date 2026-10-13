# BRC-FUNCTION-CORRESPONDENCE-01 — fresh-reader r2 clarification

**Linked reader record:** r1, SHA-256 `f12ec0e1c58251993f015846cf336ea7cdf401f5b85f9f1b92ccf81a7baec499` (preserved unchanged).

**Public PR binding:** Parm-1/Bloodborne-Research-Commons#8, observed open/draft at exact head `790ff6608cae66f8e73519932b51e4b7282c06e0` by public GitHub API. This is the requested r2 head at review time.

### Boundary wording clarification

In r1, “omits the last five possible byte starts” should be read precisely as follows: the pinned bbport scanner loop is `for i in range(len(code) - 5)` ([`tools/re/callgraph.py`, line 37 at pinned source commit `3c57da4198ad62039f63f33bfd205b9916518acf`](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/tools/re/callgraph.py#L37)). For a byte array of length N, it scans offsets 0 through N−6. Offset N−5 is the final position at which a complete five-byte E8/E9 candidate could fit, and that one valid candidate start is omitted. Offsets N−4 through N−1 are also unscanned positions, but a complete five-byte candidate cannot fit at those positions. This is a source-bound arithmetic clarification only; no scanner was executed and no candidate/result is asserted.

No other r1 finding or conclusion changes. The guide and RC-0003 already describe the one-valid-start boundary correctly.
