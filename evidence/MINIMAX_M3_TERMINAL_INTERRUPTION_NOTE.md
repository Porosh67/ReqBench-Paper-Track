# MiniMax M3 terminal interruption — operational incident and usage note

**Project:** ReqBench, Track B
**Related campaign archive:** `TrackB_192_MiniMax_M3_2026-11-12.zip`
**Related interrupted run:** `run_T08_minimax_m3_condB_rep2`
**Updated note date:** 14 November 2026

## 1. Purpose and evidence sources

This note records the MiniMax M3 campaign interruption and its resource-use context. It distinguishes (a) archive-derived run and provider-usage records, (b) the operator's contemporaneous observation of the usage display and terminal behaviour, and (c) the terminal transcript supplied after the campaign. These sources are not interchangeable.

The supplied terminal transcript includes the Windows subprocess writer-thread exception shown below. The reported 20–30 minute apparent stall and continued account/token consumption are operator observations; the supplied transcript does not itself contain a provider billing export or token-usage dashboard screenshot.

## 2. What the run archive actually records

The MiniMax M3 result JSONL contains **40 rows**, but these are two revisions for each of **20 unique run IDs**; they are not 40 distinct executed runs. The campaign plan allocated 40 M3 run slots. The archive records 20 M3 run records and 20 later slots skipped after the interruption.

Of the 20 unique observed M3 run records:

- **19** have a `provider_usage.jsonl` file with recorded usage;
- **1** interrupted record, `run_T08_minimax_m3_condB_rep2`, has no recorded usage telemetry;
- the 19 available usage files contain **485 provider-usage events**.

Summing the 19 available M3 run-level usage files gives:

| M3 campaign usage field | Archived amount | Interpretation |
|---|---:|---|
| Input/prompt tokens | 6,209,223 | Recorded input tokens across 19 M3 run records |
| Cached input tokens | 5,595,642 | A subset of the input total; do not add again |
| Output/completion tokens | 149,785 | Recorded output tokens |
| **Input + output total** | **6,359,008** | Archived subtotal for 19 M3 run records |
| Provider usage events | 485 | Events represented in those 19 usage files |

The separate, non-scored MiniMax M3 capability check has its own provider-usage file: 16 events, 67,925 input-plus-output tokens, including 57,265 cached input tokens. It is outside the 40 planned M3 campaign slots and must not be silently mixed into the scored campaign subtotal.

These archive-derived figures are more precise than a dashboard recollection, but they do not cover the interrupted run because its usage file is absent. They also do not prove that the provider dashboard's displayed usage window had exactly the same scope as the campaign archive.

## 3. Operator-observed usage display — keep separate from archive totals

The operator recalls seeing a Fireworks usage display at approximately **8 million total tokens** during the M3 campaign/stall period. This recollection refers to a total-token figure that included a cached portion; it does **not** mean that all 8 million tokens were cached tokens.

The approximate dashboard observation is not independently reconciled to the archive's 6,359,008-token subtotal for 19 M3 run records. The difference may reflect the absent usage record for the interrupted run, a different dashboard time window, or other usage included in the display; the available evidence does not determine which explanation is correct. Therefore:

- report **6,359,008 total tokens, including 5,595,642 cached input tokens**, as the archive-derived subtotal for the 19 M3 records with usage logs;
- report **approximately 8 million total tokens, with some cached portion**, only as a retrospective operator-observed dashboard figure, with its exact scope and split unreconciled;
- do not describe 8 million as cached-only tokens;
- do not add the approximately 8 million recollection to the archive subtotal or to the all-model campaign total.

## 4. Terminal condition and operator stop decision

During the final observed MiniMax M3 execution, the Windows terminal appeared to make no progress for approximately 20–30 minutes. The operator reports that automatic token/credit consumption was still continuing while the terminal remained stalled.

The supplied terminal transcript records this subprocess writer-thread exception:

```text
Exception in thread Thread-172 (_writerthread):
Traceback (most recent call last):
  ...
  File "...\\subprocess.py", line 1619, in _writerthread
    self._stdin_write(input)
  File "...\\subprocess.py", line 1155, in _stdin_write
    self.stdin.write(input)
  File "...\\encodings\\cp1252.py", line 19, in encode
    return codecs.charmap_encode(input,self.errors,encoding_table)[0]
UnicodeEncodeError: 'charmap' codec can't encode character '\\u2192' in position 1113: character maps to <undefined>
```

This identifies a local Windows process-I/O encoding failure: the `cp1252` encoder could not encode U+2192 (`→`) while a subprocess writer thread was writing input. It is distinct from model-generated invalid tool-call JSON and from turn-budget exhaustion.

**Operator clarification:** the immediate reason for stopping was the apparent terminal stall while automatic token/credit consumption continued. The operator manually stopped the campaign to prevent further uncontrolled consumption. Do not describe the primary reason as data preservation.

The campaign control log records `KeyboardInterrupt` / `operator_interrupt` at `run_T08_minimax_m3_condB_rep2`. After that event, the fail-fast control path recorded 20 `run_skipped_fail_fast` slots: four remaining T08 slots, eight T10 slots, and eight T11 slots. Those skipped slots were not provider-executed attempts.

## 5. Keep failure categories separate

1. **Invalid streamed tool-call JSON:** model/tool-call output was malformed in several recorded runs. This is not the same failure as the local Windows encoding exception.
2. **Turn-budget exhaustion:** four MiniMax M3 records reached `Maximum model-turn budget exceeded`. This is a run-state observation; it does not by itself isolate the cause of repeated turns.
3. **Command-runner friction:** the supplied run narrative describes supported-command discovery and rejected command forms. These observations show runner interaction friction, but the archive does not quantify a model-specific causal effect.
4. **Local Windows process-I/O incident:** the `cp1252` / U+2192 writer-thread exception occurred in the terminal during the final observed M3 execution.
5. **Operator stop and skipped slots:** the operator stopped the stalled campaign while usage was continuing; 20 later M3 slots were skipped by fail-fast.

The evidence does not show that the local encoding exception caused the earlier invalid JSON outputs or turn-budget exhaustion, nor does it establish that any single issue explains every incomplete run.

## 6. Interpretation boundary

- This note is an operational incident and resource-usage record, not a model-quality result.
- The 20 skipped M3 slots are unexecuted planned slots, not 20 model failures.
- The M3 archived token subtotal covers 19 run usage files, not all 20 observed M3 run records.
- The approximately 8 million dashboard figure is an operator recollection with unresolved scope and cached/input/output split; the cached portion is included in total usage, not added on top.
- No model superiority or requirement-state/patch-correctness conclusion follows from this incident.
- This note supplements the post-submission evidence companion; it does not alter the 13 November Kaggle manuscript or the original campaign archive.

## 7. Source and audit lineage

- Campaign archive: `TrackB_192_MiniMax_M3_2026-11-12.zip`
- Archive SHA-256: `d7a38ed67dcf776d28b0d041f87b9e0596d60e7e3d104dadfa5dfe8991bc55f4`
- Archived M3 result file: `minimax_m3_results.jsonl` (40 revision rows; 20 unique run IDs)
- Archived M3 per-run provider usage: 19 `provider_usage.jsonl` files, 485 events
- Operator-supplied terminal transcript: Windows writer-thread `UnicodeEncodeError` at `cp1252.py` while encoding U+2192 (`→`)
- Related public evidence: `MODEL_RUN_STATES.csv`, `CAMPAIGN_EVENTS.csv`, and `TOKEN_TELEMETRY.csv`
