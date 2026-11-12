# ReqBench experiment protocol

## Research objective

Evaluate how repository-level coding agents maintain requirement state when requirements change, while separating requirement-state fidelity from implementation correctness, regression safety, verification evidence, and cost.

## Fixed conditions

- **A — Full history:** the complete chronological requirement conversation.
- **B — Summary:** a faithful summary of the same source conversation.
- **C — Versioned ledger:** a declarative, versioned requirement-state ledger with source/transition traceability.
- **D — Ledger + bounded feedback:** a byte-identical initial ledger to C, followed by at most one researcher-controlled sanitized sealed-evaluator feedback round and one correction opportunity. D is an intervention, not a fifth representation.

## Requirement ontology

Lifecycle and role/scope are separate axes. Lifecycle values are `active`, `superseded`, and `cancelled`. Role/scope values are `ordinary`, `persistent`, and `exception`. A persistent constraint may remain active across requirement changes; an exception is scoped and does not automatically become a global rule.

## Assignment structure

Track B plans 12 Main12 tasks, 24 task–model pairs, four conditions, and two repeats: 192 planned runs with a hard ceiling of 200. Eight ceiling slots are unallocated and are not automatic retries. Model allocations are documented in the main paper and Sprint v9-derived table.

## Measurements

Measure separately: source/state traceability; active constraints and omissions; stale/superseded behavior; exception scope; patch integrity; independent acceptance and regression; public tests; sealed evaluation; evidence quality of agent claims; preparation/tool/runtime/token/monetary costs. Do not collapse these into one unvalidated composite score.

## Fairness controls

Within each task–model block, hold repository snapshot, task request, tests, runner, tool permissions, environment, and declared budget constant. Record prompt-size differences and deviations. The intended condition–repeat order is deterministic within each block, with model execution order fixed in the supplied campaign design.

## Evaluation boundary

Public tests are agent-visible. The sealed suite is intended to remain inaccessible until patch freeze. A/B/C receive no sealed outputs. D may receive at most one sanitized report only when the evaluator boundary is qualified and the procedure is authorized. Do not expose hidden tests, expected values, reference patches, gold labels, or researcher-only mappings to participants.

## Current study status

The available archive is a partial execution record. It does not contain completed independent evaluation, sealed results, or any D feedback rounds. The present report therefore does not estimate treatment effects or rank models.
