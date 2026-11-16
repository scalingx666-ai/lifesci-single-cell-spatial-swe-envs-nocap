# Issue

**Title:** Log p-values

## Description

- p-values now the result of hypergeometric test for over-representation, not under-representation
- internally calculate and work with log p-values
- add all_log_p_values_ attribute
- threshold plot to evaluate solutions at different threshold levels
- updated notebook

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a3269803733`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.