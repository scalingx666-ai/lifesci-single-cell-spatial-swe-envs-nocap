# Issue

**Title:** Alternative ways to get genomic positions

## Description

* Add tests for get_genomic_position_from_gtf
 * make gtfparse an optional dependency (it tends to make trouble)
 * implement a `get_genomic_positio_from_biomart` function and advertise it as the new default

Fix #145 -> this is also the infamous gtfparse issue
Fix #7 -> implement workaround for non-gencode GTFs; also biomart is anyway better
Fix #144 -> alternative way to get genomic positions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a293a5061af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.