# Issue

**Title:** Feature/merge new attention to code base

## Description

This is the new attention mechanism that enables controllable attention between four parts within the sequence (Cls_cell, Cls_neb, cell, neb). It also includes a fix to separate the Cls tokens.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2d7e94ff419`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.