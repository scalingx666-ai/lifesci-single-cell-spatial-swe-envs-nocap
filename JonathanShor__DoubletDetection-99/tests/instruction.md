# Issue

**Title:** Log p val

## Description

- p-values now the result of hypergeometric test for over-representation, not under-representation
- p-values calculated as log p-values
- threshold plot to evaluate solutions at different threshold levels
- updated notebook

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c951a300ed5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.