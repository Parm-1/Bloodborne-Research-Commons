# BRC-AGENT-ENTRY-USABILITY-02 observation record (reader r1)

Class S self-report. Class U fields are marked UNKNOWN.

Attempt: one fresh reader, one attempt. No retry, coaching, revision, fallback reader or model, child agent, or new-topic campaign. No memory, local repository, or inherited workspace instruction file was read.

Content-bearing invocations (each one functions.exec containing one tools.exec_command; outer and nested max_output_tokens 8000):
1. Commons START_HERE.md at 4dcb72ff; head -c 12000; complete.
2. Commons README.md; head -c 14000; complete.
3. knowledge/texture-prep-source-lifetime.md; head -c 26000 of 33681 bytes; bytes 26001-33681 not read (review-integration history tail).
4. claims/RC-0007-prep-completion.md and claims/RC-0008-map-removal-ordering.md; head -c 9000 each; complete.
5. frontiers/resource-ownership.md; head -c 9000; complete.
6. knowledge/original-code-differential-validation.md bytes 1-24000 of 34154.
7. Same file, bytes 24001-34154; complete.
8. claims/RC-0009-camera-equality.md and claims/RC-0010-differential-outcomes.md; head -c 7000 each; complete.
9. frontiers/differential-validation.md and docs/CORPUS_CHECKPOINT.md; head -c 8000 each; complete.
10. docs/CONTINUATION.md; heading list, then lines 37-82 with head -c 6500. Partial: the "Separating premises in a task answer" section was cut after its first sentence and not read further.
11. bbhost src/host/textures.cpp at 566184a7 fetched whole to scratch (4054 lines); displayed lines 1080-1135 and 1136-1170. Complete for displayed ranges; the rest of the file is in scratch and was not displayed.
12. sources/projects.yaml fetched to scratch; grep-filtered lines only (bbport, bbhost, repo, commit, license, url).
13. bbport git tree listing at 3c57da41, recursive; path names only, filtered for audio and occlusion terms. Metadata, counted conservatively as content-bearing.
14. bbport src/runtime_audio.c at 3c57da41 fetched to scratch (271 lines); grep-filtered output only, not a full read.
15. docs/SOURCE_FRESHNESS.md; head -c 7000 of 6263 bytes; complete.
16. bbhost src/host/textures.cpp scratch copy: lines 980-1000, lines 823-900 (display cut partway through PrepPool::wait), and lines 3340-3352.

Totals: 16 content-bearing invocations of 30. Truncation: three invocations were cut by my own byte caps (3, 10, 16); no harness-reported truncation. Recovery invocations: 0. Failed invocations: 0. Bookkeeping writes and hashes (this file, the answer file, and digests) are not counted as content reads.

Entry navigation: START_HERE, then README's route table, then the dossiers, claims, and frontiers the table names, then CORPUS_CHECKPOINT, CONTINUATION, and SOURCE_FRESHNESS as the allowed entry links direct. I did not follow review reports, PR pages, issue pages, historical answers, or historical usability reports. CORPUS_CHECKPOINT's current-status section and the texture dossier's header name review and reader reports by title and link; I saw those names in allowed pages but did not open them. No accidental prohibited read is known.

Timing, tokens, and effective model: UNKNOWN. Per-call wall times were sub-second to about 1.2 s; no token counts were exposed. The requested native haiku_worker identity (Claude Haiku 5.5, high) is not independently exposed to me, so the served backend is UNKNOWN.

Closure: no children spawned; no repository mutation, publication, execution, or input acquisition; no upstream action. Writes were limited to the scratch directory /tmp/brc_u02_scratch, which holds the upstream files fetched in invocations 11, 12, and 14, and to the two frozen answer files in /tmp.
