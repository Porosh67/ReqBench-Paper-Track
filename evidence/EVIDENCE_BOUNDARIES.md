# Evidence boundaries and non-claims

## What this supplement supports

1. A Track B campaign was planned with 192 scored run slots across 24 task–model assignments, four conditions, and two repeats.
2. The archived campaign accounting reports 172 unique run IDs and 20 MiniMax M3 slots skipped after an operator interruption.
3. The interruption is recorded at `run_T08_minimax_m3_condB_rep2` with `KeyboardInterrupt`/`operator_interrupt`; the 20 subsequent skipped IDs are separately enumerated.
4. Public runner observations, run-record states, and aggregate token telemetry are documented.
5. The archive-level record reports no completed independent evaluations, no sealed results, and no D feedback rounds.

## What this supplement does not prove

- It does not prove any model or condition is superior.
- It does not establish a task-resolution or agent-success rate.
- It does not establish patch correctness or regression safety.
- It does not establish requirement-state fidelity for the 172 records.
- It does not establish the effect of D feedback.
- It does not qualify the evaluator as independent or sealed; G7/G8 remain `NOT_QUALIFIED`.
- It does not make the full campaign independently reproducible from public files alone.
- It does not prove third-party rights or provider-output terms are cleared.

## Patch evidence caution

The manuscript reports that 36 records contain changed-file data and a patch hash. That is evidence of editing activity and recorded patch metadata, not evidence that the patches are correct. This supplement intentionally does not publish a patch-level inventory because the later run-to-patch reconciliation was not fully validated. In particular, a previous helper script's `0/94 evaluable patches` conclusion was defective because it never populated its patch map; that conclusion must not be treated as a result.

## Source and audit lineage

The aggregate figures are based on the private campaign archive `TrackB_192_MiniMax_M3_2026-11-12.zip` and the manuscript/evidence audit dated 13 November 2026. The archive SHA-256 is recorded in `CAMPAIGN_ACCOUNTING.md`. The source archive itself is not part of this public supplement.
