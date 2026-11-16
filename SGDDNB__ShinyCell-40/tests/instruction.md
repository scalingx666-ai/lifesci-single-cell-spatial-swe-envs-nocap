# Issue

**Title:** Fixes bug in createConfig

## Description

Hi all,

Thanks for creating this tool - very useful!

I tried to use it with a SingleCellExperiment object as input and I got an error message saying that the dimensionality reductions were not found. Looking at the code, I think this is due to a bug in the function (line 50 said sce when it should be obj).

I think this PR resolves the issue.

Best

Cata

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bfeae9ef5f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.