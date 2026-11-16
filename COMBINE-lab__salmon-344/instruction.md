# Issue

**Title:** Add option for using quante.genes.sf and to choose default value

## Description

This small patch adds two options to quant merge:
- --genes to force use of quant.genes.sf instead of quant.sf ;
- --missing <arg> to change the default value in case of missing value.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd72104684a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.