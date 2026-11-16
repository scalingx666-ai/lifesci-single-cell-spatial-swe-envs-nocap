# Issue

**Title:** h5dump and plaintext option

## Description

- store extra stuff in HDF5:
  - kallisto version
  - index version
  - call
  - start time
- add option `kallisto h5dump abundance.h5 output_dir`
  - outputs plaintext to output_dir
  - outputs run_info
- add option `kallisto h5dump --peek abundance.h5`
  - outputs metadata to stdout (extra stuff + number of targets, and number of bootstraps)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10e152eb5840`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.