# Issue

**Title:** fix: reap leaked dask workers in process-based featurization

## Description

.

`_run_tiled(..., kind="processes")` runs work on a `LocalCluster(processes=True)`. Under Python 3.14 the cluster teardown can leave worker/nanny processes alive; an orphan that inherited stdout/stderr keeps the pipe open, so a consumer waiting for EOF (the CI coverage step) hangs indefinitely.

Fix: record the cluster's own child PIDs and reap any that outlive `close()`, leaving a host app's pre-existing children untouched. `psutil` is already a `distributed` dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52856c2de5a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.