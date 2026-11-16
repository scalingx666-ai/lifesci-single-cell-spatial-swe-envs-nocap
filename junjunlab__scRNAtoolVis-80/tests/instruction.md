# Issue

**Title:** Allow per-cluster myMarkers in jjVolcano

## Description

## Summary
- `jjVolcano`'s `myMarkers` now accepts a named list of character vectors (cluster name → markers) in addition to a plain vector, letting different clusters label different gene sets.
- Updated roxygen doc and regenerated `man/jjVolcano.Rd`.

## Test plan
- [x] `jjVolcano(diffData = pbmc.markers, myMarkers = c("GeneA", "GeneB"))` still labels the same genes across all clusters.
- [x] `jjVolcano(diffData = pbmc.markers, myMarkers = list(ClusterA = c("GeneA"), ClusterB = c("GeneB")))` labels only the per-cluster genes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3ae6a478b0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.