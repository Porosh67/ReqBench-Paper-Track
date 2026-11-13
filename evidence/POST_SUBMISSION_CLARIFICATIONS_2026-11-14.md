# ReqBench Track B — post-submission clarifications

**Clarification date:** 14 November 2026
**Related manuscript snapshot:** 13 November 2026
**Campaign archive:** `TrackB_192_MiniMax_M3_2026-11-12.zip`
**Archive SHA-256:** `d7a38ed67dcf776d28b0d041f87b9e0596d60e7e3d104dadfa5dfe8991bc55f4`

## 1. Version boundary

This note records information clarified after the Kaggle manuscript was submitted. It does not revise the submitted manuscript and must not be represented as text that appeared in that submission. The 13 November paper remains a protocol and partial-execution audit; this file is a separate, dated evidence-companion update.

## 2. Cross-model operational profile

The Track B plan contains 192 run slots across 24 task–model assignments, four conditions (A/B/C/D), and two repeats. The archive contains 172 unique run IDs; 20 planned MiniMax M3 slots were skipped after the operator interruption and were not provider-executed attempts.

| Model profile | Planned / unique records observed | Awaiting independent evaluation / feedback | `run_failed` / turn-budget exhausted / interrupted |
|---|---:|---:|---:|
| MiniMax M3 | 40 / 20 | 8 / 4 | 3 / 4 / 1 |
| MiniMax M3.1 Flash | 64 / 64 | 38 / 14 | 12 / 0 / 0 |
| DeepSeek V4.1 Flash 1017 | 40 / 40 | 18 / 7 | 9 / 6 / 0 |
| GLM 5.3 Flash | 48 / 48 | 30 / 11 | 7 / 0 / 0 |
| **Total** | **192 / 172** | **94 / 36** | **31 / 10 / 1** |

The MiniMax M3 JSONL has 40 rows because each of its 20 unique run IDs has two record revisions. These are not 40 executed run IDs. The 20 remaining planned M3 slots were skipped after the interruption.

These are archive-record states, not task-correctness or success rates. M3.1 Flash has zero turn-budget-exhausted records in this archive, but it also has 12 `run_failed` records, while M3 has three; the profiles have unequal task allocations and different observed denominators. The four common assigned tasks are T02, T05, T08, and T11. Any cross-model comparison should be explicitly descriptive and restricted to matched task–condition–repeat blocks where records actually exist, with independent patch adjudication required before correctness claims. The current aggregate does not establish an overall model ranking or superiority claim.

## 3. Failure categories and interruption context

The archive records 31 `run_failed` states; the campaign audit associates most with invalid streamed tool-call JSON and one with a file-permission error. Ten records exhausted the model-turn budget: four MiniMax M3 and six DeepSeek V4.1 Flash 1017. Operator/session observations also describe command-runner friction, including command forms rejected before a supported Python invocation was found. The aggregate does not quantify this friction by model or establish how many failed runs it caused.

During the final observed MiniMax M3 execution, the operator reports an apparent 20–30 minute terminal stall. The supplied terminal transcript shows a subprocess writer-thread `UnicodeEncodeError`: Windows `cp1252` could not encode U+2192 (`→`) while writing input to a subprocess. This local process-I/O error is separate from model-generated malformed tool-call JSON and turn-budget exhaustion.

**Operator clarification (14 November 2026):** the terminal appeared stalled while automatic token/credit consumption continued. The operator manually stopped the campaign to prevent further uncontrolled consumption. The control log records `KeyboardInterrupt` / `operator_interrupt` at `run_T08_minimax_m3_condB_rep2`. After this interruption, fail-fast recorded 20 skipped M3 slots (four remaining T08 slots, eight T10 slots, and eight T11 slots). These skipped slots did not call the provider. Do not describe data preservation as the primary reason for stopping.

The available evidence does not establish that the local encoding incident caused earlier invalid JSON outputs or turn-budget exhaustion, nor that one cause explains every incomplete run.

## 4. Resource observations clarified after submission

### 4.1 Account-credit balance observations

The campaign archive's `monetary_cost` fields remain unknown/null, not zero. The operator later compared displayed USD-denominated account-credit balances:

| Observation | Displayed balance | Arithmetic |
|---|---:|---:|
| Before smoke tests | $23.48 | Operator-reported opening display |
| At start of main four-model campaign | $23.44 | After smoke tests |
| After campaign | $20.13 | Operator-reported remaining display |
| Smoke-test balance reduction | $0.04 | $23.48 − $23.44 |
| Main-campaign balance reduction | $3.31 | $23.44 − $20.13 |
| **Combined balance reduction** | **$3.35** | **$23.48 − $20.13** |

This is operator-reported balance arithmetic, not a downloaded invoice or independently reconciled billing export. It assumes no intervening top-up, refund, or account adjustment. Do not call it cash expenditure unless the payment record confirms that interpretation. No per-run monetary-cost allocation is available. These balance observations do not retroactively populate the archive's null cost fields.

### 4.2 Token usage — all-model archive total and M3 subtotal

The archive's all-model usage telemetry covers 170 run records:

| All-model campaign telemetry | Tokens | Interpretation |
|---|---:|---|
| Input tokens | 25,843,964 | Includes cached input |
| Cached input tokens | 22,601,942 | Subset of input; do not add again |
| Output tokens | 2,096,616 | Added to input for input-plus-output total |
| **Input + output total** | **27,940,580** | 170 records with usage telemetry |

A separate direct extraction of the MiniMax M3 `provider_usage.jsonl` files gives a model-specific subtotal for 19 of its 20 unique observed run records:

| MiniMax M3 archive usage | Tokens |
|---|---:|
| Input tokens | 6,209,223 |
| Cached input tokens | 5,595,642 (subset of input) |
| Output tokens | 149,785 |
| **Input + output subtotal** | **6,359,008** |
| Provider usage events | 485 across 19 run usage files |
| M3 run records without usage file | 1 — the interrupted T08/B/repeat-2 run |

The 40 M3 JSONL rows are two revisions per 20 unique run IDs. The 6,359,008-token subtotal is calculated from the 19 available unique-run usage files; it does not include a made-up value for the interrupted run. The separate non-scored M3 capability check recorded 67,925 input-plus-output tokens (including 57,265 cached input tokens) in 16 events; it is outside the scored 40-slot M3 block and is kept separate.

### 4.3 Operator-observed usage display and wall-clock duration

The operator also recalls seeing a Fireworks usage display at approximately **8 million total tokens** during the M3 campaign/stall period. This was a total-token figure with some cached input included; it was **not** 8 million cached tokens. The recalled dashboard figure has not been reconciled to the 6,359,008-token archive subtotal for 19 M3 runs. Its exact reporting window and whether it included the interrupted run or other API activity are not established. Keep it as an operator-reported dashboard observation only; do not add it to the archive totals or treat it as an exact per-run/model accounting figure.

The operator observed that the overall campaign took **more than four hours** of wall-clock time. This is not Fireworks API latency. The archive also has summed per-run elapsed fields of approximately 18,072.358 seconds (about 5.02 hours) and a median of about 70.232 seconds. The sum of per-run elapsed fields is not the same thing as campaign wall-clock duration, especially where activity can overlap.

No reliable server-side Fireworks latency measurement is present in the archive. Campaign wall-clock duration and token totals cannot be used as provider API latency estimates.

## 5. Public-disclosure boundary

The public companion contains the methodology, aggregate run states, public-test summaries, token totals, and sanitized operational evidence. It does not publish raw model conversations, per-run tool traces, raw model-response dumps, patches, private task packets, hidden tests, or evaluator assets. Aggregate API-credit consumption is resource accounting; it is not publication of raw model outputs. This observation does not itself constitute provider-issued written authorization or a legal determination about every form of systematic API benchmarking or future use.

## 6. Interpretation limits and unchanged claims

- The 127 A/B/C final-stage public-test observations and 43 D-initial observations are runner observations, not independently adjudicated task-resolution rates.
- No independent patch evaluation is complete in the archive; no sealed result is populated and no D feedback round was used.
- G7/G8 evaluator isolation and access-separation qualification remain `NOT_QUALIFIED`.
- Cross-model operational differences are descriptive. No model ranking, general superiority claim, or representation-effect estimate is supported by the current evidence.
- No single actor is assigned responsibility for every failure. The records distinguish model/tool-call output errors, budget exhaustion, command-runner friction, the local Windows process-I/O incident, and the operator's stop decision.
- The submitted 13 November Kaggle manuscript is unchanged. This note is a post-submission evidence update, not a retroactive amendment to that paper.

## 7. Source references

- [Public evidence directory](https://github.com/Porosh67/ReqBench-Paper-Track/tree/main/evidence)
- [Model run states](https://github.com/Porosh67/ReqBench-Paper-Track/blob/main/evidence/MODEL_RUN_STATES.csv)
- [Condition run states](https://github.com/Porosh67/ReqBench-Paper-Track/blob/main/evidence/CONDITION_RUN_STATES.csv)
- [Token telemetry](https://github.com/Porosh67/ReqBench-Paper-Track/blob/main/evidence/TOKEN_TELEMETRY.csv)
- [Campaign events](https://github.com/Porosh67/ReqBench-Paper-Track/blob/main/evidence/CAMPAIGN_EVENTS.csv)
- [MiniMax M3 terminal interruption and usage note](https://github.com/Porosh67/ReqBench-Paper-Track/blob/main/evidence/MINIMAX_M3_TERMINAL_INTERRUPTION_NOTE.md)
