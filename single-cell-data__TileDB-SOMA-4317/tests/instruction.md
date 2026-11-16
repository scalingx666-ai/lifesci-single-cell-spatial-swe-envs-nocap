# Issue

**Title:** [r] Fix BPCells ingestion

## Description

Address issues with BPCells ingestion by re-indexing each chunk's `soma_dim_0` from the span of the chunk matrix to the span of the input matrix. Previously, each chunk would always be written in the span of `soma_dim_0 = [0, stride]`, this needs to be fixed to be the span of the input matrix

Also add round-trip tests to ensure that the SOMA array matches the input matrix

Fixes [SOMA-719](https://linear.app/tiledb/issue/SOMA-719/bpcells-ingestion-produces-incorrect-expression-values)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04b4d451e1f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.