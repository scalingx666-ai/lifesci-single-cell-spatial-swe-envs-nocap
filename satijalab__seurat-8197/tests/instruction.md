# Issue

**Title:** Fix access to layer data for DietSeurat in V5.

## Description

This  which is caused by a change in mojaveazure/seurat-object@d6aa9af2acc999da35a82bf760ff92cca0af0854 that changed the behavior of brakets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d752a890d149`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.