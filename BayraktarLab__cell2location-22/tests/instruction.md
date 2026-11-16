# Issue

**Title:** Add SoftplusTransform

## Description

Added file `transforms.py` with `SoftplusTransform(Transform)` that transforms via the mapping `Softplus(x) = log(1 + exp(x))`. Contains inverse and `log_abs_det_jacobian` too.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65ba20c9aa83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.