# BRC-AGENT-ENTRY-01 fresh-agent reading r2 (AFFECTED SAME-READER REPAIR CHECK)

Status: AFFECTED SAME-READER REPAIR CHECK. This is one follow-up of the original exercise, not a new independent trial, and it makes no performance or causal claim. Original report r1 is immutable: /tmp/BRC-AGENT-ENTRY-01-FRESH-AGENT-r1.md, SHA256 937e14eeaecdd1071ccdd2bb211307c8af6705cf587685aa0efcad28e5aa9479. Its full text is appended verbatim at the end of this file.

Exact new public head: 4989ad73f991e15986f92bed007b12d2db1d322f
Clarified entry root: https://github.com/Parm-1/Bloodborne-Research-Commons/tree/4989ad73f991e15986f92bed007b12d2db1d322f
Earlier head used by r1: a969ab69263dd87c8c5a7845536f999a76182796

Usage and elapsed time: unknown. No scripts or code from the repository were executed. No children, external writes, game or asset acquisition, or prospective checks were performed.

## Observed navigation at the new head

1. README.md, read in full at 4989ad73.
2. START_HERE.md, read in full. Its step 4 is the clarification: name the source commit(s), platform and configuration, and any authorization, eligibility and identity-phase premise for each task answer; a field the project does not supply is UNKNOWN and must not be inferred from a nearby pin or branch.
3. llms.txt, the public index.
4. docs/SOURCE_FRESHNESS.md, read in full. Its commit-identity section is new.
5. frontiers/function-correspondence.md, read in full.
6. Public metadata tree listings for both heads, used only to compare blob identities of non-review files.

Reused by blob identity, not re-fetched at the new head: knowledge/function-address-correspondence.md, knowledge/texture-prep-source-lifetime.md, knowledge/original-code-differential-validation.md, claims RC-0003 and RC-0007 through RC-0013, frontiers/resource-ownership.md, frontiers/differential-validation.md, docs/CORPUS_CHECKPOINT.md, AGENTS.md. Their blob IDs are unchanged between the two heads, so the content read in r1 applies at the new head.

Not opened: docs/CONTINUATION.md (named by START_HERE step 3 and the README; treated as a protocol file and excluded by the task), docs/reviews/*, docs/drafts/*, the PR template or any PR body, and the other excluded files. docs/EVIDENCE_POLICY.md and sources/projects.yaml were not needed and were not opened.

## What changed between the two heads

Among non-review, non-.github files, only START_HERE.md and docs/SOURCE_FRESHNESS.md changed. The tree differs by one file under the excluded paths (reviews, drafts or .github), which I did not inspect. README.md, llms.txt, all claims, the three dossiers, the frontiers and the corpus checkpoint are unchanged.

Two repairs follow from the changes. START_HERE step 4 requires each answer to state the commit, platform, configuration and premises, with UNKNOWN for any field the project does not supply. The freshness document now separates "same commit as pin" (the resolved commit equals the registry pin) from "selected paths unchanged at another commit" (the commit differs, but each named path in that repository's scope has the same blob identity). My r1 answer to Question 4 used the phrase "checked at another revision, same commit as pin", which applied the wrong label. This is the repair.

## Original questions (verbatim from r1)

The four original questions are reproduced verbatim in the appended r1 text below.

## Revised answer 1

Source commits: bbport 3c57da4198ad62039f63f33bfd205b9916518acf for the scanner, and bbhost 566184a74f071166299bb656c4af479e5bbe2771 for the kit, address helpers and loader. Both are the registry pins, and the blobs read at the new head are unchanged. Platform: x86-64 ELF images; the kit's selected path follows Linux-style facilities (knowledge/function-address-correspondence.md). Configuration: the kit base 0x400000 is a kit convention, not a runtime slide. Authorization: source reading only. Identity premise: the input digest, build, view and segment provenance for each report are not supplied, so each is UNKNOWN.

Without those premises the two numbers only match arithmetically. The kit's 0x4035a0 minus 0x400000 equals 0x35a0, the scanner's ELF address. The guide requires an established image identity and an unambiguous, reversible segment mapping before a same-image join, and otherwise returns UNKNOWN and stops (knowledge/function-address-correspondence.md, record-and-convert table and finite workflow step 1). Replacement cannot be decided from these reports. A zero-caller result does not establish unreachability, complete decompilation or runtime equivalence, because the scanner misses indirect calls, short and conditional jumps, mid-function calls and callees without an FDE (claims/RC-0003, limits). Neither report gives an extent (claims/RC-0013).

In the hypothetical, the point conversion is supported under those premises. With offset 0x1000, vaddr 0x3000 and filesz and memsz 0x1000, the address 0x35a0 maps to file offset 0x15a0 and back, and the kit's file_at mapping agrees. The guide's decision table gives JOIN_SUPPORTED_UNDER_PREMISES for the point (decision table; claims/RC-0012). Extent, routine identity, reachability and replacement equivalence remain open. They need validated extent evidence and a separate runtime contract.

Next action: obtain the input digest, build, view and program-header table for both reports from their producers.

## Revised answer 2

Source commit: bbhost 566184a74f071166299bb656c4af479e5bbe2771. Platform: the x86-64 Vulkan host with its Linux and Windows branches (knowledge/texture-prep-source-lifetime.md). Configuration: UNKNOWN. The report does not identify the upload route (CPU async, GPU hash-only, in_vram, direct import or flexible host-pointer import), whether async is enabled, or the driver. Authorization: source reading only. Identity premise: the old hash-only job, the Surface route and the owner of the guest allocation are not supplied, so each is UNKNOWN.

The CPU batch wait establishes that the CPU-side guest reads for jobs in that batch had finished before GPU submission consumed the destination (claims/RC-0007). It orders destination consumption only. The dossier says it is not a prerequisite for guest release or the original allocator's reuse. The erase and fence establish that the submitted GPU work for that Surface completed, such as a direct-import untile read or a device-local fetch. The hash-only job is a separate CPU worker task with no batch wait, and the fence has no dependency on it. Its guest hash reads may still be running, and the inspected paths expose no post-erase receipt for it (claims/RC-0007; dossier, hash-only row).

Unresolved: the original texture owner's free and recycle rule and its writer ordering (frontiers/resource-ownership.md); the flexible host-pointer import branch; and kernel map removal, which does not wait for prep readers (claims/RC-0008). Next action: keep the allocation unreleased and check the original owner's free and recycle contract for any wait on prep readers.

## Revised answer 3

Source commit: bbhost 566184a74f071166299bb656c4af479e5bbe2771. Platform and configuration: Linux-style x86-64 SysV with AVX, default GS TLS, the kit's compile flags -fno-stack-protector and -ffp-contract=off, and -mavx on the replacement sources (knowledge/original-code-differential-validation.md, pipeline section). Input identity: the contract names a 1.09 SHA-256 starting 941f887a; the input hash used in the user's runs is not supplied, so it is UNKNOWN. Authorization: running the pair needs an authorized executable, and none is recorded, so UNKNOWN. Receipt attribution: the user's commit, blob hashes, compiler and flags are not supplied, so receipt B's attribution cannot yet be checked.

Receipt A is a skip. CMake marks exit 77 as a skip, and no frame runs (claims/RC-0010; outcomes table). The outer CTest success does not change that, and A supports no equality claim.

If receipt B's attribution is verified, it is the normal success branch and supports agreement for the selected sequence under this matrix (outcomes table). It does not establish original-world fidelity. Both arms share a collision stub that ignores world geometry, the same host math, and the same synthetic inputs (contract, step 1; claims/RC-0009). It does not establish byte identity either. Camera words, shape, matrix and cast records are compared by word or canonical NaN, and GSM compares only the first 0x20 bytes raw. Other state is excluded (quantity matrix; claims/RC-0011).

On NaN payloads, camera words and cast records treat a payload-only change as equal, while the GSM raw comparison treats it as different (quantity matrix; claims/RC-0009). The decisive check from r1 remains the one-bit finite camera perturbation with the expected gate failure. It should follow the attribution check that records receipt B's commit, hashes and flags.

## Revised answer 4

The newer bbhost branch has no recorded commit. Its platform, configuration, authorization and identity phase are all UNKNOWN. Under START_HERE step 4, none of these may be inferred from the 566184a pin or from the branch date. Classification: not checked.

Under the freshness document, the two predicates are separate. "Same commit as pin" applies only when the resolved commit equals the registry pin. "Selected paths unchanged at another commit" applies when the commit differs but each named path in that repository's scope has the same blob identity (docs/SOURCE_FRESHNESS.md, commit identity section). My r1 label "checked at another revision, same commit as pin" was wrong, because a branch with a different commit cannot carry that label. The branch can carry the selected-paths label only after its commit is recorded and the bbhost scope is compared.

The bbhost scope in the freshness worked check is eboot_kit.cpp, eboot_kit.h, insn_eboot_test.cpp, addr.h, elf.cpp, memory.cpp, memory.h and the decomp-test build settings in CMakeLists.txt. One unchanged file does not settle the question, and the date does not either. The freshness document says that age alone says nothing about semantic freshness. The bbport group is a separate comparison and is not implicated by this branch.

Smallest next action: have the project record the branch's commit, then compare only the bbhost scope against 566184a, separately from the bbport group.

The shader defect is an uncovered question. The README route table and the corpus checkpoint give other graphics and shader topics no answer or coverage status (README.md; docs/CORPUS_CHECKPOINT.md). Platform, configuration, the target commit and the shader step are also UNKNOWN. Route it as uncovered. Smallest next action: name the target commit, platform, configuration, the exact shader and translation step, and the expected versus observed output. Do not borrow the texture or camera dossiers.

Authority: the repository is a public research index with pinned sources and evidence limits. It supplies no project state and authorizes no private-project access, game execution, native or GPU work, spending or upstream action (START_HERE.md; README boundaries).

## Affected repair check: outcome

The repair changes Question 4's label and adds the per-answer premise fields that START_HERE step 4 requires. Questions 1 through 3 keep their r1 conclusions. Questions 1 through 3 gain a commit, platform, configuration and identity statement. Question 4 changes its label and its premise. The repair does not add a new source fact, runtime result, performance observation or causal claim. This record is an affected same-reader check, so it is not an independent trial.

## Original report r1 (verbatim copy, SHA256 937e14eeaecdd1071ccdd2bb211307c8af6705cf587685aa0efcad28e5aa9479)

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
