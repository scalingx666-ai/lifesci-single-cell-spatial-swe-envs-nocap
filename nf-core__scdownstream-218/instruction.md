# Issue

**Title:** Fix some minor bugs

## Description

- Prevent dedoubleted size detection if doublet detection is disabled
- Remove index name in `setindex`
- Fix scimilarity prefix to ensure compatibility with reference mapping

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29f226772494`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.