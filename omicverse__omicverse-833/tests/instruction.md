# Issue

**Title:** fix(pp): normalize CUDA devices for PyG neighbors

## Description

## Summary

- Normalize bare CUDA devices to indexed CUDA devices before PyG KNN calls `torch.cuda.mem_get_info()`.
- Reuse a lightweight helper in `_optional.py` so device normalization does not import settings or trigger settings-side effects.
- Apply the same normalization to related GPU code paths that can receive bare `cuda` devices.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90b84a651da1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.