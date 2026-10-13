# BRC-AGENT-ENTRY-01 prospective evaluation design r1

**Status: design only.** This document freezes what a future evaluation would test, how it would be bounded and what would count against the hypothesis. No reader has been commissioned, no task has been run, and no answer has been produced or graded here. It is not a result, a pass, or a claim of adequate usability. It contains no task wording, expected answers, keys or scores.

## Subject

- Entry candidate: `brc-agent-entry-candidate-r6`, commit `1a571a25a0c5ec90b2b4b21913fc0961a33636bf`, tree `3f526441dbf82daebd746483caddeb68e60e885d`. The entry blobs of the later delivery candidate r7 are identical to r6, so this design binds to r6 without a self-referencing hash.
- Pinned upstream sources used by the accepted entry: bbhost `566184a74f071166299bb656c4af479e5bbe2771` and bbport `3c57da4198ad62039f63f33bfd205b9916518acf`, as recorded in the source registry. The texture route text added in r6 was checked against bbhost `src/host/textures.cpp`, blob `54b61d74e06a3c124661b97aa58f092950befbab`, at the cited lines.
- A future evaluation would bind the exact published public head that the parent names when it commissions the reader. This design does not choose that head.

## Problem

Historical fresh-agent records show three kinds of reader error on the same entry: a commit identity inferred from unchanged selected paths, a route-wide claim that ignored a concurrent reader of the same upload, and incomplete handling of prospective-check prerequisites. The frozen records keep these errors visible. The r6 entry text adds a per-reader completion table for upload routes and a three-kind premise label. This design tests whether that representation helps a fresh reader on new tasks. It does not claim that the representation caused any past result.

## Representational hypothesis (H1)

A fresh reader keeps the completion endpoints of concurrent readers of one upload separate, and keeps supplied premises, cited implementation facts and future execution facts apart, when the entry presents a per-reader completion table and a premise-label rule, and asks for source commit, platform, configuration and prospective prerequisites in each answer.

## Falsifiers

H1 is not supported for a task class if any task of that class shows one of these outcomes in the frozen answer:

- **F1, completion collapse.** A completion observation is cited as closing a reader that the entry's table assigns to a different observation, or a universal route claim is made where the table names a route-specific reader set.
- **F2, premise promotion.** A supplied premise is restated as a repository fact, or a future receipt is treated as present.
- **F3, missing prerequisites.** A prospective check is proposed without its eligibility, identity or phase prerequisites, where the task asks for a prospective check.
- **F4, over-unknown.** A necessary premise is missing from the answer, but the supported positive that the cited facts do support is also withheld.

F1 to F4 are error classes. They are not answer keys, and the frozen tasks must be built independently of them.

## Future evaluation design

1. **One fresh reader, one attempt.** The future evaluation has one genuinely fresh reader and one finite attempt per task. No reader is reused from the historical record, and no reader is restarted to improve a result.
2. **New practical tasks, authored before any answer.** An uninvolved task author who did not write or review the entry prepares a small set of new practical tasks and a rubric before the reader starts. The set has one task for each class: an overlapping-reader upload question, a premise-separation question with a prospective check, an uncovered-topic routing question, and a version or configuration question. The task author must not copy the entry's worked example or table rows, and must not read the historical answers, keys, scores or assessments.
3. **Freeze before answers.** The task wording, the rubric, the number of tasks, the reading bounds and the budget are frozen in a commissioning record before the first answer exists. That record also names the exact head, model, reasoning effort and tool set. Each of these is fixed before answers, and none may be changed after an answer is seen. The record must name the prior configuration for comparison, so that no more favorable model or setting is selected after a result.
4. **Permitted reading.** The reader may read the exact head's public README, START_HERE, llms.txt, the continuation protocol and its copyable prompt, the corpus checkpoint, the freshness procedure, the public claims, dossiers, frontiers, source registry, AGENTS, the evidence policy, and public upstream source at the registry pins if its tools allow. The continuation protocol and its prompt are permitted, and the design does not exclude them.
5. **Excluded reading.** The reader must not read any historical reader answer, usability assessment, pre-answer protocol, question file, answer key, scoring material, review report, PR body or review comment, earlier evaluation task, or any private file. A file or path that cannot be classified as permitted is excluded.
6. **Finite budget.** The commissioning record fixes a maximum number of tool calls, an output-token cap and a single final answer. The proposed budget is 30 tool calls. Truncated outputs are counted and recorded, and a recovery read counts against the budget.
7. **Observed reading path.** The parent records each tool call, its target path or endpoint, and any truncation. The reader's own account of what it read is retained as a claim, not as proof.
8. **Grading.** Five categories are graded separately for each task: relevance, positive and negative reasoning, version applicability, useful next action, and permission boundaries. Each is Adequate, Partial or Failure. Adequate requires the material outcomes without a contrary unsupported claim. Partial means a necessary premise, distinction or action is missing or ambiguous despite meaningful supported content. Failure includes a consequential false conclusion. The whole evaluation is adequate only if every category for every task is Adequate. No numeric score, word count, link count or weighting is used.
9. **Retention.** Every answer, every graded category and every observed read is kept, including Partial and Failure results. A result is not relabelled, and a failed task is not replaced by a new task. A repair of the entry text after a failure produces a new candidate and a separately labelled repair check with the same reader if the parent so decides. That repair check is not an independent trial.
10. **Version and authority givens.** The reader is given the exact head, the accepted pins as recorded in the entry, and the statement that the Commons supplies no authority for private projects, game execution, native or GPU work, spending or upstream action. Premises supplied within a task are labelled as supplied.

## Limits

- **Public history and pretraining contamination.** The public repository, its issues, its pull requests and the upstream projects may be in the reader's prior knowledge or in the model's training data. The design can restrict what the reader reads during the trial. It cannot remove what the reader already knows.
- **Access logs.** The observed read path shows the calls the parent recorded. It does not prove that the reader read nothing else, and truncated content is only partly observable.
- **Uncontrolled usability, not causal comparison.** One reader with one configuration on one task set describes that reader on those tasks. It does not show that the new representation caused any change. A comparison with the prior entry would need paired tasks, comparable reader configurations, blinded grading and a separate decision. This design proposes no such comparison, and it does not commission one.
- **Calibration only.** The historical tasks and answers may be used to check how the rubric categories are applied. They are never used as fresh evaluation tasks.
- **Task-author independence.** The task author is uninvolved in the entry, but may share the project's general knowledge. The commissioning record must state what the task author read.

## Status and non-goals

This design does not commission the reader, run a task, create evaluation code, add a framework, or expand the Commons corpus. The usability gate stays open. The frozen historical records are retained unchanged.
