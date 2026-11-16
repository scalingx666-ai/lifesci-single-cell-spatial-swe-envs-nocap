# Issue

**Title:** update ReadParseBio to be compatible with latest split-pipe v1.1.0

## Description

Hi Seurat Team!

In the latest version of split-pipe (v1.1.0) from Parse Biosciences the `DGE.mtx` file name changed to `count_matrix.mtx`. This change breaks the `ReadParseBio()` so I modified the function to be compatible with both file name types.

I hope you can incorporate the change to the next Seurat update!

Best,
Efi

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `443ab8668425`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.