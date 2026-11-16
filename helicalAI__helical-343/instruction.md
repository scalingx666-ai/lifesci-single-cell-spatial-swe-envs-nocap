# Issue

**Title:** Bug fix: TF surgery

## Description

Current implementation permutes indices of special tokens:
```
[START]: 2 -> 1
[END]: 3 -> 2
[RD]: 4 -> 3
[CELL]: 5 -> 4
[PAD]: 1 -> 5
[MASK]: 6 -> 6
```
This fix makes sure we preserve the indices
of the special tokens when performing vocabulary surgery.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a5ff4715a52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.