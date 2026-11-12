# Reproducibility and artifact boundary

This public package provides the paper, protocol description, and aggregate execution summaries. It does not contain the original task repositories, condition input packets, agent conversations, patches, tool traces, hidden tests, sealed evaluator, or per-run raw records. Therefore, a reader can inspect the protocol and reported archive-level accounting but cannot independently reproduce the full scored campaign from this repository alone.

The aggregate CSV files were generated from the archived campaign JSONL files by grouping on `run_id` and retaining the latest revision. The source archive had 344 JSONL rows for 172 unique run IDs. The private source archive is intentionally not included in this public package.

## Before attempting a confirmatory run

1. Close the G7/G8 evaluator isolation and access-separation qualification, or formally exclude sealed/D procedures from the authorized scope.
2. Freeze and verify the final assignment manifest and source hashes.
3. Resolve the T05 durable-audit semantics mismatch and T04/T05 mutation-to-assertion traceability issues.
4. Stabilize streamed tool-call JSON handling, test import/collection, turn budgets, and permission handling.
5. Capture patch hashes, public-test commands/results, independent sealed adjudication where authorized, D feedback evidence, model/runtime identity, and token/cost telemetry.
6. Report any deviations and missing records; never impute skipped or missing runs.

## Recomputing the included aggregate tables

The supplied tables are archival summaries. The private source archive contains internal data not suitable for public release; this package intentionally does not ship a parser for those private records or a row-level export.
