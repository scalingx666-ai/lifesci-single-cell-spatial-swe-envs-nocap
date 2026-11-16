# Issue

**Title:** Quality AddModuleScore_UCell

## Description

In some limited testing I did locally, it seemed like users of scGate needed to manually call "library(UCell)" before using scGate. I dont see any imports in NAMESPACE, so this PR qualifies UCell::AddModuleScore_UCell, which I think might fix this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f51fde32cffb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.