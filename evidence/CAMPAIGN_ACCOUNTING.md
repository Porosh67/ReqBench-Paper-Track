# Track B campaign accounting

## Campaign design

| Item | Recorded value |
|---|---:|
| Planned scored runs | 192 |
| Campaign ceiling | 200 |
| Task–model assignments | 24 |
| Conditions | 4 (A/B/C/D) |
| Repeats per task–model–condition | 2 |
| Main12 tasks approved | 12/12 |
| Preflight task–condition package checks | 48/48 PASS |
| Roster validation | `CONFIG_AND_MANIFEST_PASS` |

The eight slots between the 192-run plan and the 200-run ceiling were unallocated headroom, not automatic retries.

## Observed archive

| Item | Recorded value |
|---|---:|
| Unique run IDs with records | 172 |
| JSONL revision rows | 344 (two revisions per run ID) |
| Planned slots not executed | 20 |
| Completed independent evaluations | 0 |
| Populated sealed-evaluation results | 0 |
| D feedback rounds used | 0 |
| Runner tool events | 2,650 |
| Records with token-usage telemetry | 170 |

The four result JSONL files contain 20 MiniMax M3, 64 MiniMax M3.1 Flash, 40 DeepSeek V4.1 Flash 1017, and 48 GLM 5.3 Flash unique run records.

## Latest run-record states

| State | Count |
|---|---:|
| Awaiting independent evaluation | 94 |
| Awaiting one sanitized feedback round | 36 |
| Run failed | 31 |
| Turn budget exhausted | 10 |
| Interrupted | 1 |
| **Total** | **172** |

These are record states, not success/failure rates for the underlying coding tasks. In particular, `awaiting_independent_evaluation` means adjudication remains pending.

## Public-test observations

- A/B/C final-stage observations: 127 (52 exit 0, 46 exit 1, 29 exit 2).
- D initial-stage observations: 43 (14 exit 0, 19 exit 1, 10 exit 2).
- All 29 A/B/C exit-2 observations were reported as test collection/import errors.
- No D final-stage observations are recorded.

Exit code 0 is not an independently adjudicated task-resolution result. Exit code 1 records a test failure in the captured workspace. Exit code 2 records collection/import errors and should not be merged with ordinary functional test failures.

## Tool and patch telemetry

The manuscript reports 2,650 tool events, 30 failed runs associated with invalid streamed tool-call JSON, and one file-permission error. Ten runs exhausted the model-turn budget. Thirty-six records included changed-file data and a patch hash; this indicates editing activity, not patch correctness. This supplement does not publish per-run patch mappings or claim that all patch hashes have been independently reconciled.

## Campaign interruption

The event log records a `KeyboardInterrupt`/`operator_interrupt` at `run_T08_minimax_m3_condB_rep2`. The campaign then emitted 20 `run_skipped_fail_fast` events. The exact skipped MiniMax M3 IDs are listed in `SKIPPED_MINIMAX_M3_RUNS.csv`. These are unexecuted slots, not 20 model failures.

## Archive identity

| Property | Value |
|---|---|
| Source archive | `TrackB_192_MiniMax_M3_2026-11-12.zip` |
| Byte size | 8,874,974 bytes |
| ZIP entries | 5,401 |
| CRC check | PASS (reported) |
| SHA-256 | `d7a38ed67dcf776d28b0d041f87b9e0596d60e7e3d104dadfa5dfe8991bc55f4` |

The source archive is private and is not included. The SHA-256 string is a fingerprint for verifying a separately obtained copy; it is not a substitute for access to the archive.
