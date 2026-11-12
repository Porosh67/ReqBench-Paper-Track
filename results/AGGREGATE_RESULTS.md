# Aggregate execution summary

**Source snapshot:** `TrackB_192_MiniMax_M3_2026-11-12.zip`  
**Archive SHA-256:** `d7a38ed67dcf776d28b0d041f87b9e0596d60e7e3d104dadfa5dfe8991bc55f4`  
**Aggregation rule:** deduplicate JSONL by `run_id`, retain the highest `record_revision` (then latest `record_updated_at`). Raw run-level records are not included in this public release.

## Campaign accounting

| Measure | Count / state |
|---|---:|
| Planned scored runs | 192 |
| Campaign ceiling | 200 |
| Unique run IDs with records | 172 |
| Unexecuted/skipped after operator interruption | 20 |
| JSONL rows before deduplication | 344 (two revisions per run ID) |
| Independent-evaluation completions | 0 |
| Sealed-evaluation records populated | 0 |
| D feedback rounds used | 0 |
| Runner tool events | 2,650 |
| Records with usage telemetry | 170 |

## Latest run-record states

| State | Count |
|---|---:|
| Awaiting independent evaluation | 94 |
| Awaiting one sanitized feedback round | 36 |
| Run failed | 31 |
| Turn budget exhausted | 10 |
| Interrupted | 1 |
| **Total unique records** | **172** |

## Public-test observations

A/B/C contribute 127 final-stage observations: **52 exit 0, 46 exit 1, 29 exit 2**. All 29 exit-2 A/B/C records are test collection/import errors in the captured output. D contributes 43 initial-stage observations: **14 exit 0, 19 exit 1, 10 exit 2**. No D final-stage observation is present. These are runner observations, not adjudicated task-resolution rates.

## Model allocation versus observed records

See `model_execution_summary.csv`. The 40-run MiniMax M3 block contains 20 records because the campaign was stopped during that block; the remaining 20 were skipped. The other three model blocks contain the planned counts. This is not a balanced or completed four-model comparison.

## Token telemetry

| Measure | Total |
|---|---:|
| Input tokens | 25,843,964 |
| Cached input tokens (subset of input) | 22,601,942 |
| Output tokens | 2,096,616 |
| Input + output tokens | 27,940,580 |
| Monetary cost | Unknown / null (not zero) |

## Interpretation boundary

These aggregates describe execution feasibility and archive accounting only. There are no completed independent evaluations, no sealed outcomes, and no delivered D feedback intervention. Exit-code-0 counts must not be called agent success rates. No representation-effect estimate, model ranking, or sealed correctness claim is supported by this archive.
