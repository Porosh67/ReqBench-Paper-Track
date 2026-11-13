# ReqBench — Public Evidence Supplement

**Snapshot date:** 13 November 2026  
**Campaign:** Track B, 192 planned runs  
**Source archive:** `TrackB_192_MiniMax_M3_2026-11-12.zip` (private; not included)

This directory supplements the existing paper companion with structured, sanitized evidence summaries. It does not replace or modify the manuscript, protocol, aggregate results, or reproducibility note already in the repository.

## What is included

- `CAMPAIGN_ACCOUNTING.md` — planned-versus-observed campaign accounting and evidence boundaries.
- `MODEL_RUN_STATES.csv` — latest run-record states by model profile.
- `CONDITION_RUN_STATES.csv` — latest run-record states and public-test observations by condition.
- `PUBLIC_TEST_OBSERVATIONS.csv` — aggregated public-test exit-code observations by condition and stage.
- `SKIPPED_MINIMAX_M3_RUNS.csv` — the 20 MiniMax M3 slots recorded as skipped after the operator interruption.
- `CAMPAIGN_EVENTS.csv` — the interruption and fail-fast skip event summary.
- `TOKEN_TELEMETRY.csv` — token usage totals and coverage.
- `SECURITY_AND_GOVERNANCE_STATUS.md` — G1, G7/G8, rights, and evaluation qualification status.
- `EVIDENCE_BOUNDARIES.md` — what this public supplement proves and does not prove.
- `FILE_SHA256SUMS.txt` — SHA-256 checksums for the files in this supplement, excluding the checksum file itself.

## Important interpretation

The campaign archive contains 172 unique run IDs from 192 planned slots. The 20 skipped MiniMax M3 slots were not model calls and must not be counted as failed model executions. The interruption itself occurred in `run_T08_minimax_m3_condB_rep2`; it is distinct from the 20 skipped slots.

The archive contains no completed independent-evaluation outcomes, no populated sealed-evaluation results, and no delivered D feedback rounds. Public-test exit codes are runner observations, not task-resolution rates. No A/B/C/D treatment effect or model ranking is established by this evidence.

## Privacy and redistribution

This is a sanitized aggregate supplement. It intentionally excludes raw conversations, per-run tool traces, patches, task packets, repository snapshots, hidden tests, expected outputs, evaluator assets, credentials, and private filesystem paths. The private source archive is not included. Third-party rights and applicable provider-output terms remain under review; no redistribution rights are granted by this supplement.

## Recomputability

The tables record reported archive-derived aggregates and event IDs from the research audit. The underlying private archive is needed to independently recompute them. The published archive SHA-256 is an integrity fingerprint only; it does not reveal or provide access to the archive contents.
