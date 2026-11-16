# Issue

**Title:** [python] Fix old `pyarrow` bug triggers

## Description

**Issue and/or context:** Fix varying dependency tests where latest pyarrow accepted code does not work on old versions o pyarrow

**Changes:**

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a60c8f13fe9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.