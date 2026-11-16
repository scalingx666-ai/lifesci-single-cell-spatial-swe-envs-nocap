# Issue

**Title:** Switch PS genotype field type to Integer.

## Description

The VCFv4.3 specification lists this field as an Integer. I ran into this issue trying to merge calls from several callers, the octopus calls disagree with the field type which causes problems when merging. Thanks so much!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed4cdef6dfc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.