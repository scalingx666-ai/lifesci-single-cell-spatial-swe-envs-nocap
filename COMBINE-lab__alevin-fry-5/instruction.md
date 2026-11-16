# Issue

**Title:** merging common bootstrapping option to develop branch

## Description

Basic bootstrapping options 

- `-b, --num-bootstraps` - specify the number of bootstraps, creates `bootstraps.eds.gz` if `--summary-stat` is not specified
- `--summary-stat` - when specified this will create `bootstraps_mean.eds.gz` and `bootstraps_var.eds.gz`, this option only creates these two files and does not write `bootstraps.eds.gz`
- `--init-uniform` - specify the way for initializing the starting values for the bootstrap

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b84a8cd4d98`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.