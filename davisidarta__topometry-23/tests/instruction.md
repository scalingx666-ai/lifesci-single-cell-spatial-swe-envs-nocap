# Issue

**Title:** Add domain checks for sparse Poincaré distance

## Description

## Summary
- implement `sparse_poincare` with safeguards for invalid Poincaré ball inputs
- register the new metric in `sparse_named_distances`

## Testing
- `python -m pytest`

------
https://chatgpt.com/codex/tasks/task_e_68bb84ced010832c98d3e62ebd19d6a2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a376c3c78fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.