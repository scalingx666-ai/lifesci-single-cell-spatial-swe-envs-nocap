# Issue

**Title:** fix: Support SpaceRanger v3 format

## Description

fixes: 

The format has a change in naming 

- v1: tissue_positions.csv (no header)
- v2: tissue_positions_list.csv (with header)
- v3: tissue_positions.csv (with header) (new)

Another change is header is set to 0 instead of 1. That was most likely a bug from  but it didn't show up since the spaceranger v1 datasets are at scanpy and scanpy also uses `header=0` https://github.com/scverse/scanpy/blob/f75575cac1e7f8779b33cb5570bc9c726313fd1d/src/scanpy/readwrite.py#L504

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83a11d522fa7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.