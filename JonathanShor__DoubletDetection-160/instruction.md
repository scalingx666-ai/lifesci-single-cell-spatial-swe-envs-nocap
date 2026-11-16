# Issue

**Title:** Use hatch instead of poetry and bump minimum versions

## Description

- Use hatch (as has become standard in scverse)
- Bump minimum versions to modern versions
- Drop non-required deps. Users can manually install leiden or louvain if they use non default args

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `420387a013a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.