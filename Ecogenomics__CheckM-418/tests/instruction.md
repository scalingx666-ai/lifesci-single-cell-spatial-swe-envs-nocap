# Issue

**Title:** Modified pysam import to class attribute

## Description

It should resolve pysam import problem when using `checkm coverage`.

Related to #413, #415, #401

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c11fed446ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.