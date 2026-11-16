# Issue

**Title:** Speed up clustering of large UMI bundles

## Description

Avoid repeatedly scanning earlier UMIs and rebuilding adjacency coverage. Track both incrementally while preserving clustering results and ordering.

Synthetic benchmarks showed **34× faster directional clustering**, **22× faster dense adjacency clustering**, and **5.3× faster complete deduplication** (13.25 → 2.51 seconds). All compared output records matched. Small real-data fixtures showed unchanged runtime.

New tests are included in CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c457eefc5e0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.