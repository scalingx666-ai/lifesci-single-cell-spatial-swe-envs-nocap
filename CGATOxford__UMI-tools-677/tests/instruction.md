# Issue

**Title:** Update _dedup_umi.pyx

## Description

UMI_tools doesn't run on my linux with the following error:
AttributeError: `np.Inf` was removed in the NumPy 2.0 release. Use `np.inf` instead.

replacing np.Inf fixed the problem

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae1e875f8cb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.