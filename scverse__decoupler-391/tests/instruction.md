# Issue

**Title:** build: require scverse-doc 0.4

## Description

0.4.0 renders math at build time with math-core instead of MathJax.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95a23962adba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.