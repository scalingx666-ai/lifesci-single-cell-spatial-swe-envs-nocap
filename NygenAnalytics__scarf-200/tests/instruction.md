# Issue

**Title:** Cytebase: paced job submission under rate limit

## Description

## Summary

A full CELLxGENE build (1,369 datasets) crashed before processing a single dataset. The orchestrator
submitted every dataset at once: for each one it read the record and wrote `_internal/pipeline.json`
twice, about 4,100 Hub calls in a few minutes. The account's API quota is 1,000 calls per 5 minutes.
A 429 on the Xet token request then left the process-wide Xet session unusable, and every later
bucket write failed with "Previous task error". This PR makes submission gradual, moves run
coordination off the bucket, and makes Xet 429s recoverable.

## Job submitter

- The orchestrator (`run_pipeline`) queues all datasets in memory. It spawns a `process_dataset`
  worker only when a container slot is free, using an `asyncio.Semaphore(PROCESS_CONTAINERS)`, and
  only after the pacer allows the next start.
- Long datasets hold their slots, and short ones are spaced out, so throughput adapts to the mix
  without bursts.
- Workers load their own records. The orchestrator no longer reads every record up front.
- Run and worker state (claims, call IDs, ownership) lives in a new `cytebase-runs` Modal Dict, not
  in `pipeline.json`. Worker ownership checks and reset read the Dict, so they use no Hub quota.
  `pipeline.json` is written twice per run, at start and at the end.
- An unregistered dataset ID is reported as an ordinary `failed` outcome. It no longer blocks the
  run.

## Pacer

- `_StartPacer` spaces dataset starts at least `300 × 40 / (0.8 × quota)` seconds apart: 15 s at
  1,000, 5 s at 3,000, 2.5 s at 6,000.
- This assumes about 40 Hub API calls per dataset (measured at about 35), and spends 80% of the
  quota so catalog updates and status reads fit in the rest.
- The quota is set at deploy time with `--hub-api-quota` (env `CYTEBASE_HUB_API_QUOTA`, default
  1000). Read it from the token's `ratelimit-policy` response header.

## Also included

- `retry()` treats hf_xet `RuntimeError`/`ConnectionError` failures (429, network, "Previous task
  error") as transient. It replaces the global Xet session before backing off (60, 120, 240 s).
- The orchestrator logs a progress line each minute (done, running, queued, outcomes, rate, ETA),
  and the final log line includes elapsed time.
- Conversion skips a source `X_umap` that Scarf cannot import (non-finite values, wrong shape or
  dtype) instead of failing the whole dataset. The skip is logged and recorded in
  `conversion.skippedEmbeddings`. Several Visium datasets were failing for this reason.

## Compatibility

- Worker reservations no longer pin `datasetVersionId`; a worker processes the registered version
  it loads.
- Reset uses the run store for child call IDs. A run started by the previous deployment can still be
  reset once its workers have drained.

## Testing

- Cytebase suite: 1,020 passed.
- New tests cover:
  - pacing and the concurrency limit;
  - a fixed number of `pipeline.json` calls per run;
  - ownership and reset through the run store;
  - Xet retry with session replacement;
  - progress logging;
  - the `--hub-api-quota` flag;
  - UMAP skipping.
- Full suite before the UMAP change: 7,421 passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3a1578c1695`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.