# Issue

**Title:** Incorporate learned fragment length distribution

## Description

In #25, @pmelsted implemented learning the FLD. Here, we compute the mean FL and incorporate it into the effective lengths.

We also no longer require the user to pass `-l`, though, if the user passes it in, then it will not compute the mean of the distribution.

In the future we should consider support for single-end reads which would require the user passes in `-l`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d86c463901c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.