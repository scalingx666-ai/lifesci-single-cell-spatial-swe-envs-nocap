# Issue

**Title:** Rename hugging-face organization (backward compatible)

## Description

Moved huffing face organization from `MICS-Lab` to `prism-oncology`. See new org [here](https://huggingface.co/prism-oncology).

Loading a model from the previous organization name should still work (added to the tests).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17a681261f88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.