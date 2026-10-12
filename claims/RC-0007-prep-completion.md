# RC-0007 — CPU batch submission wait does not include GPU hash-only prep

**Level:** SOURCE_INSPECTED. **Subject:** bbhost `566184a74f071166299bb656c4af479e5bbe2771`, texture preparation and Vulkan submission. **Checked:** 2026-10-12. **Reviewer:** pending at BRC-PREP-OWNERSHIP-01 r1 freeze.

CPU async upload adds its shared prep to `g_batch_preps`; submission waits every entry to pool state 2 before GPU consumption. GPU-route hash-only upload submits to the same pool and attaches to Surface but does not add to that batch. Its guest hashes complete when that prep's `run_prep` ends and state 2 is published, or an actual wait finishes; a GPU submission/fence alone is not that completion.

**Source/method:** read complete producer, pool/wait and consumption bodies: [upload](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L1101-L1151), [pool/read/settle](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L823-L976), [batch](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/textures.cpp#L3344-L3351), [submit](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/src/host/gpu.cpp#L5197-L5227).

**Meaningful negative:** hash-only state 0/1 with Surface erased after GPU submit is not changed to state 2 by erase; queue/worker still owns the prep. A CPU waiter may run state 0 itself or join state 1; normal wait returns only after reads. Nonqueued inline CPU prep finishes before return despite state remaining 0. These are source deductions, not executed cases.

**Exclusions/unknowns:** raw guest allocation retention, permitted writer/version interval, game reachability, all shutdown paths and GPU driver behavior. **Reuse/ownership:** KNOWLEDGE_REFERENCE; droogie/bbhost, declared GPL-3.0-or-later in [registry](../sources/projects.yaml); no code imported. **History:** new atomic r1 finding; accepted GX claims preserved. Detail and original-producer limit: [dossier](../knowledge/texture-prep-source-lifetime.md).
