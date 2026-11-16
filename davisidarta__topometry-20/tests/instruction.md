# Issue

**Title:** Simplify ANN backends and add grid search evaluation

## Description

## Summary
- limit ANN support to HNSWlib and optional NMSlib, removing redundant backends
- add `grid_search` helper to benchmark ANN graphs against exact neighbors

## Testing
- `python -m py_compile topo/base/ann.py`
- `pytest`

------
https://chatgpt.com/codex/tasks/task_e_68bb6cd819e8832cb595fffc2b6e4b55

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a04ee28a0577`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.