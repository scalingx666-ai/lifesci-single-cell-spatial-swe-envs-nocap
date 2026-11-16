# Issue

**Title:** Check sampling method in sampling file conversion script

## Description

As pointed out in #58 the format of Gibbs samples file and Bootstrap samples file is different. Here I check the `meta_info.json` file for which format should be read.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65b56ac2591f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.