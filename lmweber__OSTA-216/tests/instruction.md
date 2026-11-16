# Issue

**Title:** seq-workflow-visium-hd revision

## Description

Mainly code formatting (for consistency with guidelines), added references (Banksy, RCDT, Statial), and fixed plot description. NOTE: There is a bug in `Statial` that I reported to their GH; this PR provides a temporary workaround as I don't see this being fixed soon (package is failing to build for other reasons already)... I assume GHA are passing because we have not rebuild dependencies in a while, but I am not sure. They are not passing on my fork. So I'd be okay with merging this as is & removing the workaround when `Statial` is ready.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `510d2aec94a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.