# Issue

**Title:** Clonal cluster

## Description

* `clonalCluster()` now passes the tight similarity threshold to `immApex::buildNetwork()` instead of the loose value that was refiltered afterward. The engine prunes early rather than returning a large edge list that is mostly discarded. Raw thresholds are unchanged, and cluster assignments match the previous behavior.
* `clonalCluster()` selects the edge expansion from `cluster.method`. Connected-components clustering uses the memory-efficient star expansion, which is exact for components. Community-detection methods use the full clique expansion for exact edge multiplicity.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4772479d53ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.