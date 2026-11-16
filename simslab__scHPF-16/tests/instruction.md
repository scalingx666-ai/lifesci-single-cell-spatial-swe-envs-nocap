# Issue

**Title:** Batching

## Description

* Fixed some version incompatibilities with newer scipy
* Update to joblib as external library 
* Batching  + parallel training options
* Cell-wise mean non-zero llh
* Loss smoothing options

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a29692fc053`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.