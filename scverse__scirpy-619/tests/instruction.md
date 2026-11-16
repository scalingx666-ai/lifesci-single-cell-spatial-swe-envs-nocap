# Issue

**Title:** add sequence read in for 10x json

## Description

Previously, full nt or aa tcr sequences from 10x contigs are not being read in by `read_10x_vdj`. This PR adds those attributes when read from 10x json output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `660268998c07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.