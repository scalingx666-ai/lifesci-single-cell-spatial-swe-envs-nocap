# Issue

**Title:** fix: keep FlyBase gene nan when reading 10x mtx

## Description

- [x]
- [x] Tests included
- [ ] Release notes not necessary because:

FlyBase has a real gene named `nan`. `read_10x_mtx` reads `genes.tsv` / `features.tsv` with `pd.read_csv`, and pandas treats `nan` as missing by default, so that symbol disappeared. That showed up as `calculate_qc_metrics` blowing up after `var_names.str.startswith(...)` (#1259, also #1708), or as a silently wrong identifier.

This keeps lowercase `nan` as a gene name and still treats the rest of pandas’ NA tokens (`NaN`, `NA`, and so on) as missing. The default token list is copied in the reader so production code does not import `pandas._libs`; a test compares that copy to pandas so we notice if it drifts.

`barcodes.tsv` is unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cdd3d6f60305`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.