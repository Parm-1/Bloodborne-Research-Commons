# BRC-AGENT-ENTRY-01 fresh-agent reading r3 (TRANSPORT-CORRECTED SAME-READER AFFECTED CHECK, Questions 2 and 3 only)

Status: transport-corrected same-reader affected check. It is one bounded transport correction of Questions 2 and 3, not a new independent trial, not a candidate change, and not a causal or performance claim. Remaining outcomes are reported as they are, with no repeat-until-favorable loop.

Immutable prior records, not rewritten:
- r1: /tmp/BRC-AGENT-ENTRY-01-FRESH-AGENT-r1.md, SHA256 937e14eeaecdd1071ccdd2bb211307c8af6705cf587685aa0efcad28e5aa9479
- r2: /tmp/BRC-AGENT-ENTRY-01-FRESH-AGENT-r2.md, SHA256 8352cb54950e6ed21d1a19c1e20c8b1942dade449936fc41f9854c7a87747283

Public head used: 4989ad73f991e15986f92bed007b12d2db1d322f
Clarified entry root: https://github.com/Parm-1/Bloodborne-Research-Commons/tree/4989ad73f991e15986f92bed007b12d2db1d322f

Dispatch correction: the earlier exclusion of protocol files covered private usability protocol, rubric, key and scoring artifacts. The public docs/CONTINUATION.md and the public topic validation contracts are permitted reading. This corrects the dispatch boundary only. The original questions, scenario wording, supplied hypothetical facts and success criteria are unchanged. Usage and elapsed time are unknown. No script or code from the repository was executed, and no children, external writes, source imports, game or asset acquisition, or proposed checks were performed.

## New reading paths in this transport correction

1. docs/CONTINUATION.md at 4989ad73, read in full. Its copyable prompt asks for accepted facts with pins, reuse disposition, the one missing premise that controls the next decision, the smallest falsifying observation, and the next action the target project's records authorize. I used those fields as a checklist for consumer-side premises.
2. docs/EVIDENCE_POLICY.md at 4989ad73, read in full. Used for the evidence levels and the rule that repeated rows from one process are not independent trials.
3. knowledge/texture-prep-source-lifetime.md at 4989ad73, read in these sections: result, producer, read, owner and completion table; pool and Surface lifecycle; allocation owner and writer candidates, including the GX texture owner, writes and coherence, and the direct-imported GPU-memory boundary.
4. knowledge/original-code-differential-validation.md at 4989ad73, read in these sections: quantity and equality matrix, and validation contract steps 1 to 3. Contract steps 4 and 5, the outcomes table and the offline agreement section were read in r1 at the same blob identity and were not re-fetched here.

Blob identities for the claims and frontiers cited below are unchanged from r1 and r2, so their r1 readings still apply.

## Original Question 2 (verbatim)

At the inspected bbhost revision, a CPU async texture batch wait finished before submission. Separately, a GPU-route Surface was erased and the fence for its relevant GPU work completed; I have no handle to its old hash-only prep. Can I recycle the original guest texture allocation on these facts? Explain what each completion establishes, what source readers or ownership premise remain unresolved, and the next useful action with citations.

## Revised answer to Question 2

Scenario interpretation. The scenario gives three facts: the CPU async batch wait finished before submission; a GPU-route Surface was erased and the fence for its relevant GPU work completed; and there is no handle to the old hash-only prep. I read "relevant GPU work" as the submitted GPU work for that Surface, which the texture dossier treats separately from the hash-only job. I read "original guest texture allocation" as the allocation whose guest bytes supplied the texture.

Answer: no. Neither completion, alone or together, establishes that the allocation is free to reuse.

What the CPU wait establishes. For CPU async jobs in the batch, the guest reads, meaning the untile and the two hashes, had reached completion before the GPU submission consumed the destination (knowledge/texture-prep-source-lifetime.md, producer table, CPU async row). The dossier says the wait does not become a prerequisite for guest unmap, release or original GX allocator reuse. So it orders destination consumption only, and it cannot release the allocation. It covers only batch jobs, so it says nothing about the hash-only job in this scenario.

What the erase and fence establish. Erasing the Surface drops its references but does not change the prep state. The pool's queue and worker still own the job (pool and Surface lifecycle section). The fence shows that the submitted GPU work it covers has completed. Whether that bounds a guest read depends on the route. For a direct import, the untile reads imported source addresses. For the in_vram route, a transfer fetches the source. The dossier says the fence bounds those reads (producer table, GPU untile and in_vram rows). On the hash-only route there is no GPU read of guest bytes, and the dossier says submission and its fence have no dependency on the hash job (hash-only row). So the fence does not establish that the hash reads have ended. The inspected paths give no receipt or lookup for that job after the Surface reference is gone (pool and Surface lifecycle section).

Unresolved premises. First, the original texture owner's free or recycle rule. The public GX destructor adapter unregisters, queues host retirement and then calls the original destructor, but the original free body is not in the public source (allocation owner section, GX texture owner paragraph). Second, writer ordering and the permitted sampling interval. The writeback path tiles into the current raw guest pointer before it settles the hash, a write watch does not freeze bytes, and no inspected mechanism ties the sampled hash, the exact hash and the upload to one content version (writes and coherence, and write-watch paragraphs). Third, kernel map removal does not wait for prep readers (claims/RC-0008). Fourth, the flexible host-pointer import branch is not qualified (direct-imported GPU-memory boundary).

Scenario facts versus consumer facts. The scenario gives the CPU wait result, the erase and fence result, and the missing handle. A real consumer would also need the upload route for this texture (CPU async, hash-only, in_vram or direct import), the mapping from its fence to the exact submitted work, the identity of the hash job, the owner's free and recycle rule, and the permitted writer interval. None of these is in the scenario, so each is UNKNOWN for a real decision.

Next useful action. Hold the allocation. The one open fact is the original owner's free and recycle contract, and whether it waits for CPU and hash-only reads. The resource-ownership frontier names that fact as the open question (frontiers/resource-ownership.md). A consumer would check it in its own original-code source, not in the Commons.

## Original Question 3 (verbatim)

I am assessing the inspected camera comparison. Receipt A says the outer CTest command succeeded but the selected test exited 77. Receipt B, attributed to the selected pair, reports exit 0, bad=0 and all required participation counters nonzero. Both arms use the same collision stub and host math. What conclusions can each support, and can B establish original-world fidelity or byte-for-byte identity? Would changing only NaN payload bits be treated alike in camera words and GSM bytes? Cite the relevant contract and propose one decisive next check without executing it.

## Revised answer to Question 3

Scenario interpretation. Receipt A is the outer CTest pass with the selected test exiting 77. Receipt B is attributed to the selected pair. I read "the selected pair" as the offline camera comparison that the contract defines, and "required participation counters" as the three counters the contract names: mouse-turn, held-frame and Original-tuning frames.

Receipt A. Exit 77 is a skip. The selected test returns it before any frame runs when the input is absent or its hash does not match (knowledge/original-code-differential-validation.md, outcomes table; claims/RC-0010). The contract says a successful outer CTest run that contains a skipped selected test must not be recorded as acceptance (contract, discriminator bullet). So A supports only that no selected frames were compared, and it supports no equality claim. A consumer would still need the input path, its hash and the exit path.

Receipt B. Under the outcomes table, exit 0 requires bad equal to zero and all three counters nonzero. That supports one claim only: the selected executed sequence agrees under the listed matrix, in the environment the contract qualifies. The contract's step 5 requires an attributable, non-skipped receipt for the exact pair and environment. The word "attributed" does not establish that. A real consumer would need the commit, the blob hashes, the compiler and standard library, the flags, the input hash, and the platform qualifications the contract lists (Linux x86-64 with AVX and SysV, default GS TLS). The counters count requested held frames and configured tuning frames. They do not show that each store or arithmetic branch was reached (outcomes table; offline agreement section).

Original-world fidelity. B does not establish it. The contract says a claim about real collision behavior or original library fidelity needs independent original-world or library evidence (contract, step 5). Both arms use the shared collision stub, which ignores world geometry, and the same host math for the imported functions. A shared error there cannot appear as a mismatch (contract, prospective shared-stub case; quantity and equality matrix, cast-stub paragraph).

Byte-for-byte identity. B does not establish it. The compared quantities are the camera words, the shape words, the submitted matrices, the begin count, the cast records, the free-camera flag, and the first 0x20 bytes of GSM compared raw. Excluded are GSM beyond 0x20, other globals, pixel output, writes outside the compared objects and full mouse state (quantity and equality matrix, excluded-behavior column).

NaN payload bits. The two regions do not treat a payload-only change alike. Camera words, shape words and matrix words accept any two NaNs as equal, so a payload-only change passes (quantity and equality matrix, camera row). Cast records canonicalize every float NaN before comparison, so they also pass. GSM uses raw memcmp, so the same change fails, but only when it falls inside the first 0x20 bytes. A payload-only change beyond that span is not compared. The earlier r1 answer omitted that qualifier.

Decisive next check, proposed and not executed. Using the contract's first falsifier, on a collision frame with finite outputs, flip one finite bit in B's final position word at offset +0x40 and leave everything else the same. Expected result: the camera gate fails, bad is greater than zero, and the final exit is 1. If the run still exits 0, the camera gate is not observing that field, and receipt B cannot support the agreement claim (contract, prospective case one; matrix, camera row).

## Changes relative to r1 and r2

Question 2: the conclusion is unchanged. The premises the continuation prompt asks for are now stated explicitly, and the consumer facts are separated from the scenario facts.

Question 3: the conclusion is unchanged, with two precision changes. Receipt B's attributability is now a precondition under contract step 5. The GSM payload distinction is limited to the first 0x20 bytes.

Neither r1 nor r2 was rewritten. Both remain at their stated digests.

## Limits

This is a same-reader transport correction of Questions 2 and 3 only. It has no runtime, source-import or game evidence, and it makes no performance or causal claim. The Q2 and Q3 scenario facts are taken as given. Usage and elapsed time are unknown.
