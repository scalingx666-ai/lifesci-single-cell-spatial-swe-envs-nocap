# Issue

**Title:** Threshold plot fix

## Description

- Makes threshold plot more interpretable, removes natural log option
- Threshold plot is created much faster with new defaults
- Changes `p_thresh` default to 10e-8

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c856a24ce158`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.