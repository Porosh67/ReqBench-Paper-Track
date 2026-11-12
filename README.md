# ReqBench — Paper Track Companion

**Research title:** *When Requirements Change: Evaluating Requirement-State Representations and Test-Grounded Feedback in Coding Agents*  
**Release date:** 13 November 2026  
**Status:** Paper and partial-execution companion; not a completed benchmark leaderboard.

ReqBench studies how repository-level coding agents handle changing software requirements while preserving persistent constraints, rejecting superseded behavior, respecting scoped exceptions, and producing verifiable patches.

## What is in this repository

- `paper/` — full paper text plus formatted PDF and editable DOCX copies.
- `docs/` — experiment protocol, requirement-state ontology, contribution disclosure, and governance notes.
- `results/` — archive-derived aggregate execution summaries (no row-level run records).
- `figures/` — conceptual diagrams for the two-axis requirement-state model and A/B/C/D protocol.
- `reproducibility/` — exact boundary of what can and cannot be independently reproduced from this public release.

## Main design

The study compares four fixed conditions: **A**, full chronological conversation; **B**, faithful summary of the same history; **C**, declarative versioned requirement ledger; and **D**, a byte-identical initial C ledger plus at most one sanitized, researcher-controlled evaluator-feedback round.

The requirement ontology deliberately separates lifecycle (`active`, `superseded`, `cancelled`) from role/scope (`ordinary`, `persistent`, `exception`).

## What the current archive supports

The Track B plan contains 192 scored runs across 24 task–model assignments, four conditions, and two repeats, with a 200-run ceiling. The supplied archive has 172 unique run IDs; 20 planned runs were skipped after an operator interruption. The run records contain no completed independent evaluation, no sealed outcomes, and no delivered D feedback round. Public-test exits are execution diagnostics, not task success rates. See `results/AGGREGATE_RESULTS.md`.

**No model ranking, representation-effect estimate, sealed correctness result, or claim that D improved outcomes is supported by the current partial archive.**

## Current model allocation

MiniMax M3 (40 planned), MiniMax M3.1 Flash (64), DeepSeek V4.1 Flash 1017 (40), and GLM 5.3 Flash (48). The current archive contains 20, 64, 40, and 48 unique records respectively; the M3 block was interrupted and 20 of its planned runs were skipped. This is not a balanced completed four-model comparison.

## Contribution and governance

The Main12 research direction and non-coding work were researcher-originated/performed. Detailed task specifications were AI-assisted and researcher-reviewed/approved; coding implementation was AI-assisted under researcher direction. AI systems are not human authors. The researcher remains responsible for claims and analysis. Third-party dependency/asset rights and applicable provider-output terms remain under review; authorship clarity must not be mistaken for full rights clearance.

Security records: 25 PASS, 1 INCONCLUSIVE, 2 NOT_TESTABLE. Operational decision: `PROCEED_WITH_DOCUMENTED_LIMITATIONS`; security qualification: `NOT_QUALIFIED`. G7/G8 independent isolation/access-separation attestations have not passed.

## Important exclusions

This public companion intentionally excludes Main12 source projects, task packets, raw conversations, patches, per-run traces, evaluator/hidden-test material, reference patches, internal audit bundles, credentials, and private workspace paths. The repository does not claim those materials are cleared for public redistribution.

## Reproducibility

This repository supports inspection of the protocol and archive-level aggregate accounting. It does **not** contain enough source artifacts to independently rerun the full experiment. See `reproducibility/REPRODUCIBILITY.md`.

## Citation

See `CITATION.md`. Add a DOI only after a real DOI has been issued.

## License

No license is granted by this repository. See `RIGHTS_AND_PUBLICATION_NOTES.md`.
