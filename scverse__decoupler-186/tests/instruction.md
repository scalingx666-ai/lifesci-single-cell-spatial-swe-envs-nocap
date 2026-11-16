# Issue

**Title:** make igraph optional

## Description

Hey @PauBadiaM,

great job on the decoupler refactor. I have one more small issue with the license. Since `igraph` is a mandatory dependency, the whole package would be considered `GPL`. If you make `igraph` optional, this wouldn't be the case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da398b927c88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.