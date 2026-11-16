# Issue

**Title:** Fix FindConservedMarkers meta method labels

## Description

## Summary

- name the combined p-value column after the supplied `metap` method instead of the default formal argument
- resolve exported `metap` functions by identity so stored function references receive the correct label
- add regression coverage for direct and stored non-default methods while preserving the default label

## Tests

- focused `FindConservedMarkers` regression test with `pbmc_small`
- parsed the modified source and test files successfully

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25d4772843e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.