# Issue

**Title:** nuclei -> "nuclei"

## Description

It was throwing an "UndefVarError" for nuclei when I added nuclear and cytoplasm genes. After adding parentheses it worked fine.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2f591644364`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.