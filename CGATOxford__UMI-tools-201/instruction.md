# Issue

**Title:** {ts} debug bc pattern2

## Description

Multiple debugs for use of  `--bc-pattern`. The most worrying is that when using `--bc-pattern` and `--bc-pattern2`, the number of bases removed from read2 = len(pattern) not len(pattern2)! (9354d2660425eea58e459b17ffbb834ab7c45455) This is obviously not a problem when pattern and pattern2 are the same length, as is frequently the case, but the user will be unaware of this issue, unless pattern2 is longer than pattern in which case an error will be thrown.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `616b9d0067d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.