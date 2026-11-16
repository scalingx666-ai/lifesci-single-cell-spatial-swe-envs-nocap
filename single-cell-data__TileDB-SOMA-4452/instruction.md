# Issue

**Title:** [r] Close measurement collection handle in SummarizedExperiment ingest path

## Description

**Issue and/or context:** [SOMA-951]

**Changes:**

- Close measurement collection handle in SummarizedExperiment ingest path that prevented new measurements from being registered in resume mode
- Add test for multi-measurement `SummarizedExperiment` ingestion

**Notes for reviewers:** The [initial CI failure](https://github.com/single-cell-data/TileDB-SOMA/actions/runs/24894303302) was caused by a test that tripped a second issue in this code path, which is addressed separately in #4453. Once this is merged I'll migrate the test to that branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1542bb1709cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.