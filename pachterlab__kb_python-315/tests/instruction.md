# Issue

**Title:** Nac workflow kb ref bug fix

## Description

Fixed a NAC workflow bug where genes with no transcripts caused duplicate FASTA entries, corrupting the kallisto index and slowing bustools. The fix is ref.py.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e88ecbf0e430`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.