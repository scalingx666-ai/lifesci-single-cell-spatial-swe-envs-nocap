# Issue

**Title:** Fix negative length vectors are not allowed

## Description

Aggregate indices as list inside data.table and extract them as vector using unlist().
This . This happens when the data.table contains too many elements and somehow internally exceeds the 32 bit integer limits. By grouping the indices per RG as list we avoid the data.table growing too much.

Since the targetN is already set to 0 if it is NA in the operation before, I removed the na.omit. Also since the targetN is the same for every RG (due to rbinom(1,nmax,mean(exn)/mean(n) returning a single number) I removed the median computation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82cfafe0b718`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.