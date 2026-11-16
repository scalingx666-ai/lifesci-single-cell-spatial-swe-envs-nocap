# Issue

**Title:** `parallelize` sets numba cores to 1

## Description

Fixes 

I test this with this script: https://gist.github.com/selmanozleyen/d130bca5bd1d549e96e6664d93c70fb6

I will create mock functions that utilize parallelize with different parameters (like `use_runner` arg of `parallelize`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b74755fffb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.