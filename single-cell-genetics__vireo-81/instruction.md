# Issue

**Title:** Version less memory intensive and better MT handling + merge bams w/o vcf

## Description

This Pull Request contains:

- reduction of memory consumption
- multi threading based on splitting the positions and number of input files
- option `--merge` when no input vcf is use to still use the synth polling 
- option `--shuffle` to shuffle the input positions (makes each thread length more uniform)
- option `--test` to run only a subset of positions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `701274d6c7a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.