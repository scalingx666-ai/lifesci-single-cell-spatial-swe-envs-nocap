# Issue

**Title:** Ensure sparse gradients use data dtype

## Description

## Summary
- Use input dtype for temporary arrays in sparse operations
- Compute sparse correlation and canberra metrics using consistent dtype

## Testing
- `pytest`

------
https://chatgpt.com/codex/tasks/task_e_68bb86f56868832c90dfd102df3f083f

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9d2b84faae8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.