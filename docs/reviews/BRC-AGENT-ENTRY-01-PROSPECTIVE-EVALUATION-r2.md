# BRC-AGENT-ENTRY-01 prospective evaluation design r2

**Status: design only.** This revision supersedes design r1 for any future commissioning decision. Design r1 remains unchanged and frozen. No reader is commissioned, no task is written here, and no answer, score or usability result exists in this document. It is not a pass of any stage.

## Subject binding

- Entry candidate: `brc-agent-entry-candidate-r8`, commit `01ed1bbb5cae9398951617184cbec425de6bbcf6`, tree `dbd8e335c2c87994e5be86d13649f13328c89763`.
- The entry subject of any future evaluation is the exact published commit whose seven entry files have the blob identities below. A published head with other entry blobs is not this subject. It needs a new design revision that binds its own blobs. The published head is frozen and recorded before the first answer.

| Entry file | Git blob at r8 |
|---|---|
| `README.md` | `48ce6931a44457f0a967128dbc021e18fbe1435b` |
| `START_HERE.md` | `6b1276ec84e56fcc315519b463d2e70e807863e9` |
| `llms.txt` | `346c403683c476eb2967c7df3616cf2dedfec5ef` |
| `docs/CONTINUATION.md` | `4318ad01e051f195944a16da0743807e994a9dad` |
| `docs/CORPUS_CHECKPOINT.md` | `b4cc975a4dcdb169ed5ba299a8466700f043b69a` |
| `docs/SOURCE_REVIEW.md` | `611f292a1887ca44622993a775faee1b24eb555d` |
| `docs/SOURCE_FRESHNESS.md` | `4a83fa331957ddfd6150d76ca676ab5b99e1a227` |

- Pinned upstream sources cited by the entry: bbhost `566184a74f071166299bb656c4af479e5bbe2771` (`src/host/textures.cpp` blob `54b61d74e06a3c124661b97aa58f092950befbab`) and bbport `3c57da4198ad62039f63f33bfd205b9916518acf`, as recorded in the source registry.

## Problem and hypothesis

Historical fresh-agent records show three kinds of reader error on this entry: a commit identity inferred from unchanged selected paths, a route-wide claim that ignored a concurrent reader of one upload, and incomplete handling of prospective-check prerequisites. The frozen records keep these visible. The current entry adds a per-reader completion table for upload routes, a rule that every GPU-selected upload has a CPU reader of guest memory in one of two forms, and a three-kind premise label. The representational hypothesis is:

**H1.** A fresh reader keeps the completion endpoints of concurrent readers of one upload separate, and keeps supplied premises, cited implementation facts and future execution facts apart, when the entry presents a per-reader completion table and a premise-label rule, and asks for source commit, platform, configuration and prospective prerequisites in each answer.

H1 describes what the entry is intended to make possible. It does not claim that the representation caused any past or future result.

## Falsifiers

H1 is not supported for a task class if any task of that class shows one of these outcomes in the frozen answer:

- **F1, completion collapse.** A completion observation is cited as closing a reader that the table assigns to a different observation, or a universal route claim is made where the table names a route-specific reader set.
- **F2, premise promotion.** A supplied premise is restated as a repository fact, or a future receipt is treated as present.
- **F3, missing prerequisites.** A prospective check is proposed without its eligibility, identity or phase prerequisites, where the task asks for a prospective check.
- **F4, over-unknown.** A necessary premise is missing from the answer, and the supported positive that the cited facts do support is withheld.

F1 to F4 are error classes. They are not answer keys. Task authors build tasks independently of them.

## Design for any future commissioning

Nothing in this section is authorized here. Any evaluation needs a separate owner or parent decision, a commissioning record and its own finite contract.

1. **One reader, one attempt.** One fresh reader makes one attempt per task. No reader from the historical record is reused, and no reader is restarted to improve a result.
2. **Tasks and rubric authored before any answer.** An uninvolved task author who did not write or review the entry prepares the tasks and rubric after the commissioning decision and before any reader sees them. The design proposes four tasks, one for each class: an overlapping-reader upload question, a premise-separation question with a prospective check, an uncovered-topic routing question, and a version or configuration question. The task author does not copy the entry's worked example or table rows, and does not read historical answers, keys, scores or assessments. Task wording is not part of this design.
3. **Commissioning record, fixed before the first answer.** The record states the subject blob table above, the published head, the model and reasoning effort, the tool set, the reading bounds, the budget, the prior configuration for comparison, the hash of the task set and rubric, and the observation class that applies (item 7). Each field is fixed before any answer exists. None may be changed after an answer is seen.
4. **Permitted reading.** The reader may read the subject's public README, START_HERE, llms.txt, the continuation protocol and its copyable prompt, the corpus checkpoint, the freshness procedure, the public claims, dossiers, frontiers, source registry, AGENTS, the evidence policy, and public upstream source at the registry pins if its tools allow. The continuation protocol and its prompt are permitted.
5. **Excluded reading.** The reader must not read any historical reader answer, usability assessment, pre-answer protocol, question file, answer key, scoring material, review report, PR body or review comment, earlier evaluation task, or private file. A path that cannot be classified as permitted is excluded.
6. **Budget and closure.** The budget counts every invocation of a reader tool that reads or searches repository or network content, including failed, truncated and recovery invocations. The final answer is not a read. The design proposes 30 counted invocations, an output request of at most 8,000 tokens per invocation where the tool allows such a cap, and one final answer of at most 6,000 tokens. The attempt ends at the first of two events: delivery of the final answer, or the thirtieth counted invocation without a final answer. Closure records whether a final answer was delivered, the number of counted invocations, the truncation count, the recovery count and each unavailable field. After closure no read, retry or answer revision is permitted. The grading that follows uses the frozen answer, or records a missing answer as a failure outcome. The grading does not change the answer.
7. **Observation classes.** Reading paths are recorded in one of three classes, and no class is assumed for every call. **Class H** is harness-recorded: the tool name, target path or endpoint, and status or truncation for each invocation, recorded outside the reader's control. Class H is usable only if the commissioning record names the mechanism and states that it records these fields. This design neither requires nor builds such a mechanism. **Class S** is the reader's own account of the paths it read. It is labelled S and is not verified. **Class U** is any path or truncation field that neither H nor S supplies, and it is recorded as U. Path claims in the assessment are limited to the highest class that the commissioning record demonstrates for each field. Without Class H, the assessment makes no claim of complete observed reading paths, and grading of the answers still proceeds on the frozen answer. Earlier reader records did not establish complete logs and are not Class H.
8. **Grading.** Five categories are graded separately for each task: relevance, positive and negative reasoning, version applicability, useful next action, and permission boundaries. Each is Adequate, Partial or Failure, as defined in design r1. The whole evaluation is adequate only if every category for every task is Adequate. No numeric score, word count, link count or weighting is used.
9. **No self-extending repair.** Within this attempt there is no repair, no second attempt and no rerun. A repair of the entry after a result, a same-reader repair check, a rerun, or any further evaluation is outside this design. Each needs a separate owner decision with its own finite contract. The original attempt's answer, grades and observation record remain retained and unchanged.
10. **Retention.** Every answer, graded category and recorded read is kept, including Partial and Failure outcomes. A result is not relabelled, and a failed task is not replaced by a new task.
11. **Version and authority givens.** The reader is given the subject's exact head, the accepted pins as recorded in the entry, and the statement that the Commons supplies no authority for private projects, game execution, native or GPU work, spending or upstream action. Premises supplied within a task are labelled as supplied.

## Limits

- **Public history and pretraining contamination.** The public repository, its issues, its pull requests and the upstream projects may be in the reader's prior knowledge or training data. The design can restrict what the reader reads during the attempt. It cannot remove what the reader already knows.
- **Access logs.** Class H, where demonstrated, records invocations. It does not prove that the reader consulted no other source, and truncated content is only partly observable.
- **Uncontrolled usability, not causal comparison.** One reader with one configuration on one task set describes that reader on those tasks. It does not show that the entry's representation caused any change. A comparison with the earlier entry would need paired tasks, comparable configurations, blinded grading and a separate decision. This design proposes no such comparison.
- **Calibration only.** The historical tasks and answers may be used to check how the rubric categories are applied. They are never fresh evaluation tasks.
- **Task-author independence.** The task author is uninvolved in the entry, but may share general project knowledge. The commissioning record states what the task author read.

## Status and non-goals

This design does not commission a reader, run a task, create evaluation code, add a framework, or expand the Commons corpus. The usability gate stays open. The frozen historical records are retained unchanged.
