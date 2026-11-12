# When Requirements Change: Evaluating Requirement-State Representations and Test-Grounded Feedback in Coding Agents

**Subtitle:** A controlled representation-comparison protocol and an interrupted four-model execution audit

**Project:** ReqBench — Requirement-State Representation and Test-Grounded Verification in Coding Agents  
**Manuscript date:** 13 November 2026  
**Evidence cutoff:** Track B archive `TrackB_192_MiniMax_M3_2026-11-12.zip`

## Abstract

Repository agents must handle requirements that change over time while other constraints remain active. They may follow superseded rules, omit persistent constraints, overextend exceptions, or produce wrong patches despite describing the current requirements correctly. ReqBench compares four representations/interventions for the same chronological history: full conversation (A), faithful summary (B), declarative versioned ledger (C), and the byte-identical initial ledger plus one bounded, researcher-controlled sealed-feedback round (D). It measures requirement-state fidelity, patch correctness, public-test behaviour, sealed outcomes, and cost separately.

Track B allocates 12 original tasks to 24 task–model assignments, four conditions, and two repeats (192 planned runs; 200 ceiling). The supplied archive contains 172 unique run IDs; 20 MiniMax M3 runs were skipped after an operator interruption. It records 127 final A–C public-test observations (52 exit-0, 46 exit-1, 29 exit-2) and 43 initial D observations. These are execution diagnostics, not resolution rates. No sealed results or D feedback rounds are recorded. Token telemetry covers 170 runs and totals 27.94 million input-plus-output tokens; monetary cost is unknown. This is a protocol and partial-execution audit, not a treatment-effect study or model ranking.

## 1. Introduction

Requirements evolve: defaults are replaced, features cancelled, exceptions scoped, while compatibility or audit constraints persist. Agents must recover the governing state, not merely retrieve an earlier instruction. ReqBench separates **requirement-state fidelity** (which rules are active, superseded, cancelled, persistent, or scoped) from **implementation fidelity** (whether the patch implements that state without regressions). A correct explanation can accompany a wrong patch, and passing visible tests may miss omissions or unseen regressions.

The primary question is how representations of the same chronological requirement history affect state fidelity, patch correctness, verification behaviour, evidence claims, and cost under controlled repository tasks. The ontology keeps **lifecycle** (`active`, `superseded`, `cancelled`) separate from **role/scope** (`ordinary`, `persistent`, `exception`).

The fixed conditions are: **A**, full chronological history; **B**, faithful summary of that history; **C**, declarative, versioned ledger with source and transition links; **D**, the byte-identical C ledger plus one sanitized sealed-evaluator report after the initial patch is frozen, with at most one correction. D is an intervention, not a fifth independent representation. Comparisons are intended within task–model blocks, not as a general leaderboard.

## 2. Related work and research position

Prior work already covers much of this territory. MemoryCode tests multi-session instruction retention [1]; Supersede studies temporal fact updates in agent memory [2]; and work on stale instruction files shows agents following obsolete repository guidance [3]. SWE-ContextBench compares reuse of coding trajectories and summaries [4], while ContextBench measures context exploration and use [5]. FeatureLoop, MACBench, FeatureArc, and EvoCode-Bench study evolving requirements, persistent workspaces, cumulative checks, repair, and regression [6–9]. LedgerBench examines executable requirement-test ledgers and obsolete-check pressure [10]; FeatureBench develops test-driven feature-level repository tasks [11]. SWE-RPG supplies intermediate ground truths for requirement clarification and planning alongside executable patch evaluation [12].

Accordingly, ReqBench does not claim to be the first evolving-requirements benchmark, requirement ledger, feedback/hidden-test design, or separation of requirement reasoning from patch success. Its provisional distinction is a controlled, within-task comparison of four representations/interventions applied to the same chronological update history, with explicit lifecycle/scope labels and separate state, patch, test, sealed-evaluation, and cost measures. Artifact-level comparison with the closest systems remains necessary before novelty can be claimed.

## 3. Research design

### 3.1 Tasks and assignment structure

Track B uses 12 original, researcher-directed Main12 tasks (T01–T12). The manifest assigns 24 task–model pairs, each expanded into four conditions and two repeats (eight runs per pair): 192 planned runs under a hard ceiling of 200. The remaining eight slots are unallocated headroom, not automatic retries.

| Model profile | Provider model identifier | Assigned tasks | Pairs | Planned runs |
|---|---|---|---:|---:|
| MiniMax M3 | `accounts/fireworks/models/minimax-m3` | T02, T05, T08, T10, T11 | 5 | 40 |
| MiniMax M3.1 Flash | `accounts/fireworks/models/minimax-m3p1-flash` | T01, T02, T03, T04, T05, T06, T08, T11 | 8 | 64 |
| DeepSeek V4.1 Flash 1017 | `accounts/fireworks/models/deepseek-v4p1-flash-1017` | T02, T05, T08, T11, T12 | 5 | 40 |
| GLM 5.3 Flash | `accounts/fireworks/models/glm-5p3-flash` | T02, T05, T07, T08, T09, T11 | 6 | 48 |
| **Total** | **Four profiles** | **24 task–model pairs** | **24** | **192** |

The four planned common tasks are T02, T05, T08, and T11. Unequal assignment counts mean this is not a balanced four-model-by-twelve-task factorial; cross-model analysis is restricted to shared tasks. Within each block, condition–repeat order is deterministically shuffled using a SHA-256-derived seed; model order is fixed.

### 3.2 Inputs, controls, and measurements

Within each task–model block, conditions share the repository snapshot, task request, public tests/runner, instructions, tools, permissions, environment, and declared budget. Prompt-length differences are measured, not hidden. Measurements remain separate: requirement labels/source traceability; omissions and stale-rule behaviour; patch integrity and independent acceptance/regression; public-test commands/results; evidence-supported claims; and preparation, tool, runtime, token, and monetary cost. No composite score is used.

Public tests are agent-visible and identical across conditions for a task. The sealed suite is intended to remain inaccessible until patch freeze. A/B/C receive no sealed output; D receives one sanitized report and may correct once. `D_initial` to `D_final` is a within-run sequence, not an independent randomized contrast. `C_final` versus `D_final` compares the ledger package with the ledger-plus-feedback package and must account for D's extra information and repair opportunity.

### 3.3 Task provenance and contribution disclosure

The Main12 projects are researcher-originated and were not represented as clones or repurposed third-party repositories. The researcher originated the research direction, scope, methods, task-independence requirement, and other non-coding work. Detailed task specifications were AI-assisted and researcher-reviewed; coding implementation was AI-assisted under researcher direction. AI also assisted with manuscript drafting and data audit. The researcher remains responsible for the analysis, citations, and claims; AI systems are not human authors.

The authorship component of G1 is therefore distinct from the remaining rights review. The internal-use inventory for actual third-party dependencies/assets and applicable provider output terms is not fully closed in the records available for this manuscript. This paper does not claim that the source bundle is cleared for public redistribution.

## 4. Execution and artifact audit

### 4.1 Preflight and archive integrity

The ZIP passed its CRC check and contains 5,401 entries. The manifest defines 192 unique planned IDs; roster validation reports `CONFIG_AND_MANIFEST_PASS`, and preflight reports 48/48 task–condition package checks PASS. These establish configuration and workspace readiness, not task completion or patch correctness.

The four result JSONL files contain 344 rows: each of 172 run IDs appears as revisions 1 and 2. Deduplication yields 172 unique records, 20 fewer than planned. The event log records an operator interruption in the MiniMax M3 block and 20 `run_skipped_fail_fast` events; skipped IDs are not provider calls. Result files contain 20 M3, 64 M3.1 Flash, 40 DeepSeek, and 48 GLM records.

### 4.2 Run states and public tests

| Latest run-record state | Count |
|---|---:|
| Awaiting independent evaluation | 94 |
| Awaiting one sanitized feedback round | 36 |
| Run failed | 31 |
| Turn budget exhausted | 10 |
| Interrupted | 1 |
| **Unique run records** | **172** |

The 127 final-stage public-test observations belong to A, B, and C. Their exit-code distribution is 52 with exit code 0, 46 with exit code 1, and 29 with exit code 2. All 29 exit-code-2 records show test collection/import errors. D contributes 43 **initial-stage** public-test observations: 14 exit-code 0, 19 exit-code 1, and 10 exit-code 2. These counts describe runner outcomes at a particular patch snapshot; they are not task-resolution rates and cannot substitute for sealed evaluation. No D final-stage test result is recorded.

All 36 D records awaiting feedback report zero rounds used; the other seven D records failed. The `sealed_evaluation` field is empty in all 172 records. Thus there is no independent sealed outcome and no observed D feedback intervention.

### 4.3 Tool, patch, and resource telemetry

Runner counters report 2,650 tool events. Thirty failed runs stem from invalid streamed tool-call JSON; one reports a file-permission error. Ten runs exhausted the model-turn budget. Thirty-six records include changed-file data and a patch hash—evidence of editing, not correctness.

Token telemetry covers 170 records: 25,843,964 input tokens (22,601,942 cached) plus 2,096,616 output tokens, totalling 27,940,580. Monetary cost is unknown/null, not zero. Runtime is not comparable across this incomplete mix of failed and pending runs.

A separate, non-scored MiniMax M3 capability exercise fixed one small checkout fixture: baseline 1/6, post-patch 6/6 public tests. It is outside the 192-run denominator, used no sealed tests, and says nothing about comparative model performance.

## 5. Results and interpretation

The archive supports an execution-feasibility profile, not a ranking of A/B/C/D. Configuration validated 48 task–condition packages and the 192-run manifest. Execution produced 172 unique records, but none has a completed independent-evaluation outcome. Public-test execution appears in 170 records: 127 final A/B/C stages and 43 D-initial stages. Tool-call errors, budget exhaustion, and test import/collection errors prevent a clean outcome comparison.

The exit-code-0 observations must not be described as a 41% agent success rate: they are 52 of 127 final public-test invocations, not 52 independently adjudicated task resolutions. Similarly, exit-code-1 observations indicate test failures in the captured workspace; exit-code-2 observations indicate collection/import errors and are not interpretable as ordinary functional test failures. None of these figures establishes held-out correctness, regression preservation, or requirement-state fidelity.

Most importantly, the experiment's defining D intervention was not completed. The record shows 43 D initial test stages, 36 runs waiting for feedback, zero feedback rounds used, and no sealed results. Therefore, neither the effect of test-grounded feedback nor the relation between public and sealed performance can be estimated. Model comparisons are also inappropriate: the model blocks are unbalanced, M3 is incomplete, outcomes are pending, and the source RQ v5 describes a Gemma-specific RQ6 whereas the current Sprint v9 assigns four Fireworks model profiles. This manuscript retains the current four-model manifest as an execution descriptor but makes no Gemma-specific or model-ranking claim.

## 6. Limitations, governance, and next validation steps

The main limitation is the absence of independent evaluation: task-level requirement scores, sealed acceptance/regression results, and adjudicated patch outcomes are unavailable. Before confirmation, the harness must address invalid streamed tool-call JSON, test import/collection errors, turn-budget overruns, and the permission error. The missing M3 runs must remain missing, not be imputed.

Security records are 25 PASS, 1 INCONCLUSIVE, and 2 NOT_TESTABLE. The operational decision is `PROCEED_WITH_DOCUMENTED_LIMITATIONS`, but qualification remains `NOT_QUALIFIED`; G7/G8 isolation and access-separation attestations have not passed. No sealed-evaluation artifact appears in this ZIP, so no independent sealed-boundary success is claimed.

The 12-paper review is focused, not systematic, and not all artifacts were reproduced. Novelty remains provisional. Research_Question_v5 has a Gemma-only RQ6 that does not align with Sprint v9's four Fireworks profiles; this manuscript makes no confirmatory model-specific claim. G1 authorship provenance is disclosed, but rights for actual third-party components and applicable AI-output terms remain under review.

A confirmatory campaign should stabilize test imports, validate tool-call JSON, freeze turn/retry budgets, and preserve run-level usage/error accounting. It should complete A/B/C independent evaluation; run D only when the sealed boundary and feedback process are demonstrably permitted. T05's durable-audit requirement and T04/T05 mutation-to-assertion traceability also require reconciliation before comparative scoring.

## 7. Conclusion

ReqBench specifies a controlled way to compare conversation history, summary, a declarative versioned ledger, and a ledger with one bounded test-grounded feedback intervention while separating requirement-state fidelity from patch correctness and verification cost. The current archive demonstrates substantial implementation of the experiment harness and supplies a precise partial-execution record. It does not yet establish which representation performs best. The central scientific outcome at this stage is methodological: reliable conclusions require complete run accounting, interpretable public tests, independently qualified sealed evaluation, and an actually delivered D feedback round. Reporting these boundaries is part of the benchmark's evidence standard, not a reason to manufacture a positive result.

## References

[1] N. C. Rakotonirina et al. “From Tools to Teammates: Evaluating LLMs in Multi-Session Coding Interactions.” *Proceedings of ACL 2025*, pp. 19609–19642. https://doi.org/10.18653/v1/2025.acl-long.964

[2] V. Patel. “Supersede: Diagnosing and Training the Memory-Update Gap in LLM Agents.” arXiv:2606.27472, 2026. https://arxiv.org/abs/2606.27472

[3] X. Xu and W. Wu. “Stale Instruction Files Override the Code in Coding Agents: A One-Sentence Fix.” arXiv:2610.30571, 2026. https://arxiv.org/abs/2610.30571

[4] J. Zhu, M. Hu, and J. Wu. “SWE Context Bench: A Benchmark for Context Learning in Coding.” arXiv:2602.08316, 2026. https://arxiv.org/abs/2602.08316

[5] H. Li et al. “ContextBench: A Benchmark for Context Retrieval in Coding Agents.” arXiv:2602.05892, 2026. https://arxiv.org/abs/2602.05892

[6] J. Feng, A. Wu, C. Gao, Y. Wang, S. Lu, and Z. Hu. “Benchmarking Coding Agents under Evolving Requirements” (FeatureLoop). arXiv:2610.35488, 2026. https://arxiv.org/abs/2610.35488

[7] J. Gui et al. “MACBench: Benchmarking Multi-turn Agentic Coding with Evolving Requirements in Frontend Web Development.” *Proceedings of EMNLP 2026*, pp. 49386–49401. https://doi.org/10.18653/2026.emnlp-main.2172

[8] Y. Wang et al. “FeatureArc: Benchmarking Coding Agents on Evolving Features.” arXiv:2610.37434, 2026. https://arxiv.org/abs/2610.37434

[9] H. Shen et al. “EvoCode-Bench: Evaluating Coding Agents in Multi-Turn Iterative Interactions.” arXiv:2605.24110, 2026. https://arxiv.org/abs/2605.24110

[10] NordNeuron. “LedgerBench: An Experiment Harness for Executable Requirement-Ledger Governance.” Software repository, 2026. https://github.com/NordNeuron/ledgerbench

[11] Q. Zhou et al. “FeatureBench: Benchmarking Agentic Coding for Complex Feature Development.” arXiv:2602.10975, 2026. https://arxiv.org/abs/2602.10975

[12] X. Zhou et al. “A Unified Issue Resolution Benchmark for Requirement Clarification, Planning, and Code Generation for Coding Agents” (SWE-RPG). arXiv:2608.09072, 2026. https://arxiv.org/abs/2608.09072
