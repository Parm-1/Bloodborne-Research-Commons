# BRC-AGENT-ENTRY-01 fresh-agent reading r1

Exact public head: a969ab69263dd87c8c5a7845536f999a76182796
Entry point: https://github.com/Parm-1/Bloodborne-Research-Commons/tree/a969ab69263dd87c8c5a7845536f999a76182796

Scope: one qualitative public-source reading. No local Commons checkout, memory, chat, private BBPC material, preselected handoff, historical reader reports, rubric or protocol files, upstream script execution, binary acquisition, source import or external write was used. No children were created. This is not runtime evidence. Usage and elapsed time are unknown.

## Observed navigation (public reads only)

1. GitHub API recursive tree listing at the head, used only to enumerate paths.
2. README.md at the head, read in full.
3. START_HERE.md.
4. knowledge/function-address-correspondence.md. One short passage near the decision table was lost to tool-output truncation (about 39 tokens); the table rows were read.
5. claims/RC-0003-callgraph-limits.md, claims/RC-0012-address-coordinates.md, claims/RC-0013-unwind-provenance.md.
6. knowledge/texture-prep-source-lifetime.md, read in two passes. A middle span was truncated; the allocator-candidate paragraph was recovered by a targeted second read. The source blob table was only partly seen.
7. claims/RC-0007-prep-completion.md, claims/RC-0008-map-removal-ordering.md.
8. frontiers/resource-ownership.md.
9. knowledge/original-code-differential-validation.md, read in three passes to recover truncated spans (pipeline, inputs and loop setup, quantity matrix, outcomes, validation contract, offline agreement, source table).
10. claims/RC-0009-camera-equality.md, claims/RC-0010-differential-outcomes.md, claims/RC-0011-camera-state.md.
11. frontiers/differential-validation.md.
12. docs/SOURCE_FRESHNESS.md, docs/CORPUS_CHECKPOINT.md.
13. AGENTS.md, which the README names for agent use.

Not opened: docs/reviews/*, docs/drafts/*, docs/CONTINUATION.md, docs/EVIDENCE_POLICY.md, sources/projects.yaml, CONTRIBUTING.md, LICENSE, knowledge/gx-resource-lifecycle.md, frontiers/function-correspondence.md, and other claims outside these four questions.

## Question 1 (verbatim)

I have reports from the corpus's inspected bbport scanner and bbhost kit: scanner address 0x35a0 with no callers, and kit address 0x4035a0. Neither report records the input image digest or view. What can I say now about correspondence and replacing that code? In a separate hypothetical subcase, both reports establish the same digest/build, original-file views and coordinate origins, with one unambiguous file-backed executable segment (p_offset=0x1000, p_vaddr=0x3000, p_filesz=p_memsz=0x1000). Does that change the address-point answer? Cite what supports each result and name one next action.

## Answer 1

Correspondence is only a candidate. The kit address minus its base 0x400000 gives 0x35a0, the scanner's ELF virtual address (knowledge/function-address-correspondence.md, record-and-convert table, scanner and kit rows). A same-image point join needs the original image digest, build and view, documented coordinate origins, and an unambiguous reversible segment mapping. Neither report records a digest or view, so the identity premise is UNKNOWN. The guide says to return "UNKNOWN: original image identity or coordinate mapping missing" and stop, and it says a missing digest is not permission to subtract the base. The two numbers are arithmetically consistent under the kit's convention, and nothing more.

Replacement is not supported. A zero-caller result does not show unreachability, complete decompilation or runtime equivalence. The scanner misses indirect calls, short and conditional jumps, mid-function calls and callees without an FDE (claims/RC-0003, limits). Neither report gives an extent, so no routine boundary is established (claims/RC-0013).

The hypothetical changes the point answer and only that. With the same digest and build, original-file views, and the single file-backed executable segment (offset 0x1000, vaddr 0x3000, filesz and memsz 0x1000), scanner address 0x35a0 lies inside the segment. Its file offset is 0x1000 + (0x35a0 - 0x3000) = 0x15a0, and the inverse returns 0x35a0. The kit's BN 0x4035a0 minus 0x400000 gives the same 0x35a0 and the same file offset under file_at. That point becomes JOIN_SUPPORTED_UNDER_PREMISES (guide, decision table; claims/RC-0012). The zero-caller result is still uninformative, and no extent, routine identity or replacement equivalence follows. Those need an extent record, entry evidence and a separate runtime contract.

Next action: obtain from each report's producer the SHA-256 of the exact input file, the view used (original file or analysis view), and the program-header table. The guide names these as the premises required before any join.

## Question 2 (verbatim)

At the inspected bbhost revision, a CPU async texture batch wait finished before submission. Separately, a GPU-route Surface was erased and the fence for its relevant GPU work completed; I have no handle to its old hash-only prep. Can I recycle the original guest texture allocation on these facts? Explain what each completion establishes, what source readers or ownership premise remain unresolved, and the next useful action with citations.

## Answer 2

No. These two completions do not establish that the old guest texture allocation is free to reuse.

The CPU async wait establishes that, for prep jobs in the CPU async batch, the guest reads (the untile from source, then the sampled and exact hashes) had finished, state 2, before GPU submission consumed the destination (knowledge/texture-prep-source-lifetime.md, first route row; claims/RC-0007). It orders destination consumption only. The dossier says this wait is not a prerequisite for guest unmap, release or original GX allocator reuse.

The erase and fence establish less. Erasing the Surface drops its references but does not change the prep's state, and the prep stays with the pool's queue and worker (claims/RC-0007). The fence bounds the submitted GPU work for that Surface, such as a direct-import untile read or a device-local fetch from VRAM source. It does not bound the hash-only job's guest hash reads. That job has no batch wait, and submission and its fence have no dependency on it (dossier, hash-only row). The inspected paths expose no way to query the job once the Surface reference is gone, so its guest reads may still be running.

Unresolved: the original texture owner's free or recycle rule, and the writer ordering that keeps the source readable through the CPU untile, the exact hash, the hash-only read and the GPU fetch. The public GX destructor adapter unregisters, queues host retirement and then calls the original destructor, but the original allocator body is not in the public source (dossier, owner paragraph; frontiers/resource-ownership.md). Kernel map removal does not wait for prep readers either (claims/RC-0008). The flexible host-pointer import branch is also unqualified.

Next useful action: keep the allocation unreleased and run a focused source check of the original texture owner's free and recycle contract for any wait on texture prep readers. The resource-ownership frontier names that as its one open fact.

## Question 3 (verbatim)

I am assessing the inspected camera comparison. Receipt A says the outer CTest command succeeded but the selected test exited 77. Receipt B, attributed to the selected pair, reports exit 0, bad=0 and all required participation counters nonzero. Both arms use the same collision stub and host math. What conclusions can each support, and can B establish original-world fidelity or byte-for-byte identity? Would changing only NaN payload bits be treated alike in camera words and GSM bytes? Cite the relevant contract and propose one decisive next check without executing it.

## Answer 3

Receipt A is a skip, not a comparison. CMake marks exit 77 as a skip, and 77 is returned before any frame when the input is missing or its hash is wrong (claims/RC-0010; the outcomes table in knowledge/original-code-differential-validation.md). A supports only that the selected comparison did not run. It supports no equality claim.

Receipt B, if it is attributable to the pinned pair, is the normal success branch: bad is zero and the mouse-turn, held-frame and Original-tuning counters are nonzero. The contract reads this as "selected executed sequence agrees under this matrix", with no game, coverage or fidelity conclusion (same dossier, outcomes table). The held and tuning counters count requested frames, so they do not show that each store or arithmetic branch was reached.

B does not establish original-world fidelity. Both arms use the same collision stub, which ignores world geometry, and the same host math for the imported math functions. The synthetic singleton, parameters, characters and keep-out lists are shared as well (contract, step 1; claims/RC-0009; the cast-stub paragraph in the matrix section). B also does not establish byte-for-byte identity. The camera comparison covers 0x350 bytes by word, GSM covers only the first 0x20 bytes, and shape and matrix are compared by word. Pixel output, writes outside the compared objects, full mouse state and other globals are outside the comparison.

Changing only NaN payload bits is not treated alike. In camera, shape and matrix words, any two NaN words compare equal, so a payload-only change passes. Cast records canonicalize float NaNs to one pattern, so they also pass. GSM uses raw memcmp, so the same payload-only change fails. The contract calls the word-level case an intentional blind spot, not a GSM exception (quantity matrix; claims/RC-0009).

Decisive next check: on a frame that reaches the collision stub with finite outputs, flip one finite bit in B's final position word at offset +0x40, leave everything else unchanged, and run the selected pair. The camera gate must fail, bad must be greater than zero, and the final exit must be 1. If the run still exits 0, the camera gate is not observing that field, and receipt B cannot support the agreement claim.

## Question 4 (verbatim)

My project uses a newer bbhost branch but has not recorded its commit. Someone says the old address guide is current because eboot_kit.cpp looks unchanged and the branch date is newer than the corpus check. I also need an answer about a shader translation defect outside the four dossiers. How should I route both tasks from this repository, classify their applicability now, and choose the smallest next action? Cite the material you use and state what authority the repository supplies.

## Answer 4

Route the two tasks separately.

Address task: route to knowledge/function-address-correspondence.md with claims/RC-0003, RC-0012 and RC-0013. These are pinned to bbport 3c57da4198ad62039f63f33bfd205b9916518acf and bbhost 566184a74f071166299bb656c4af479e5bbe2771 (guide, source-bounds table; docs/SOURCE_FRESHNESS.md). For those commits, the guide's statements are "True at exact pin". For a newer branch with no recorded commit, they are "Not checked".

The argument from one unchanged file and a newer date does not settle this. The freshness procedure says to freeze the resolved commit and compare only the paths that can affect the claim. A changed caller, header, helper, loader, build setting or test consumer can alter the claim while eboot_kit.cpp stays the same. The date carries no freshness meaning: "age alone says nothing about semantic freshness" (docs/SOURCE_FRESHNESS.md). The scope in the worked check includes eboot_kit.h, insn_eboot_test.cpp, addr.h, elf.cpp, memory.cpp, memory.h, the decomp-test build settings in CMakeLists.txt, and bbport's tools/re/callgraph.py.

Smallest next action: record the branch's exact commit, then compare only those paths against 566184a. If none differs, record "checked at another revision, same commit as pin for the scope". If one differs, mark RC-0012 and RC-0013 as affected by an unreviewed change before reuse. Either way, the image digest and view from Question 1 are still needed.

Shader task: uncovered. The README's route table says that graphics or shader work outside the inspected paths has "No matching accepted dossier" and that the answer must not be inferred from these dossiers. The corpus checkpoint assigns other graphics and shader topics "no answer or coverage status" (README.md; docs/CORPUS_CHECKPOINT.md). The texture dossier cites the untile compute shader only for which guest reads occur and when. It does not check translation correctness, so it cannot be borrowed for this defect.

Smallest next action: state the target revision, the exact shader and translation step, the input, and the expected versus observed output. Then decide whether any inspected path is involved.

Authority: the repository is a public research index. Its claims describe only the cited public source and its stated scope (README.md, boundaries). It supplies pinned source references, evidence labels and a rule that a moving branch is a discovery source, not stable proof (AGENTS.md, steps 2 and 3). It does not supply your project's state, your branch's contents, runtime results, or any permission for private-project access, game execution, native or GPU work, spending or upstream actions (START_HERE.md, final paragraph).
