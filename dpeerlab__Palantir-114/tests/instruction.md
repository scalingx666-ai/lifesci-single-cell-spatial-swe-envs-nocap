# Issue

**Title:** Using sparse GP for gene trends

## Description

A user reported that the non-sparse GP does result in memory issues in specific cases:  This PR changes the default way to infer gene trends to Mellons sparse GP implementation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `568834c5e7c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.