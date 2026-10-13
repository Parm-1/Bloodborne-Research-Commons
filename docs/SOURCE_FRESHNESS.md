# Source version and freshness

The registry in [projects.yaml](../sources/projects.yaml) pins the exact source snapshots used by the claims. A pin answers “which bytes were inspected?” It does not name the version installed by a reader, establish the same game build, or make the whole corpus current. A check date records when someone looked; age alone says nothing about semantic freshness.

For a task that may depend on later source changes:

1. Record the target/project revision and exact task scope. Read the registry pin and the claim's producer, decisive consumer, and dependency/configuration paths.
2. Resolve the relevant public ref once and record its name, returned commit and check time. Freeze that commit for the comparison; do not compare one file at a moving branch head.
3. Compare only paths that can affect the claim: producer, consumer/caller, address or data conversion, dependencies, and relevant build/configuration. An unchanged headline file does not rule out a changed caller or setting.
4. Record one of these meanings:
   - **True at exact pin:** the statement is supported by the inspected source at its cited commit, within its stated scope. This is not a claim about a different revision or game behavior.
   - **Checked at another revision:** the named paths were read or compared at a separately frozen commit. State whether a relevant difference was found and leave semantic interpretation at the claim's evidence level.
   - **Affected by an unreviewed change:** a relevant path/dependency/configuration differs; applicability needs follow-up. The difference does not by itself make the older finding false.
   - **Not checked:** no valid source comparison was completed; give the exact access or scope limitation.

If revisions differ, keep the old pin and assess applicability. Do not silently replace the registry pin, infer a new source meaning, or use a recent date as a “current” badge. A changed source may leave a bounded claim unaffected, but that conclusion requires checking its actual producer and decisive consumer/dependency/configuration scope. No comparison here establishes runtime, native, GPU or game behavior.

## Bounded worked check: RC-0012/0013

**Question and scope.** Do the selected public producers and consumer used for the address-coordinate and unwind-provenance claims differ at the current default branch refs? The comparison concerns bbport's scanner and bbhost's selected kit/parser, coordinate helpers, loader, address-report consumer and relevant test configuration. It does not ask whether either tool is correct for another image or whether its report is complete.

**One ref read.** At `2026-10-13T00:52:47Z`, one `git ls-remote --symref ... HEAD` read per public repository returned:

| Repository | Ref name returned | Commit returned | Accepted registry pin |
|---|---|---|---|
| `deadinside28/bloodborne_pc` | `refs/heads/master` | `3c57da4198ad62039f63f33bfd205b9916518acf` | `3c57da4198ad62039f63f33bfd205b9916518acf` |
| `droogie/bbhost` | `refs/heads/master` | `566184a74f071166299bb656c4af479e5bbe2771` | `566184a74f071166299bb656c4af479e5bbe2771` |

Both frozen commit identities equal the accepted pins. Therefore the selected paths at those returned refs are the same committed source trees as the reviewed pins: no changed-path follow-up is indicated for these claims by this check. The named bbport producer is `tools/re/callgraph.py`. The bbhost scope is `tests/decomp/eboot_kit.cpp`, `tests/decomp/eboot_kit.h`, `tests/decomp/insn_eboot_test.cpp`, `src/engine/addr.h`, `src/core/elf.cpp`, `src/core/memory.cpp`, `src/core/memory.h`, and the relevant decomp-test build/configuration in `CMakeLists.txt`; the selected consumer and limits are described in [the correspondence guide](../knowledge/function-address-correspondence.md). Commit identity establishes these paths are unchanged from those pins; it does not show that they are valid for a reader's image, target, build options or runtime.

**Result and limit.** Record this as **checked at another ref, same commit as pin** for the selected RC-0012/0013 scope. It is not a whole-corpus freshness result or a semantic “current” badge. No registry row changed. No other branch/tag, path, dependency outside that named scope, build environment, executable/image, output, runtime, native fixture or game was checked. No upstream tool was executed. The registry YAML was not edited or parsed as part of this check.
