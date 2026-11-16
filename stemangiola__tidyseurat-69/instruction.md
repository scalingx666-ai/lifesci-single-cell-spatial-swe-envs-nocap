# Issue

**Title:** Allow to select a slot (e.g. scaled, raw etc..) in join_features()

## Description

@stemangiola 

I have made the following changes to `join_features()` and checked that `R CMD CHECK` does not produce any warnings or errors. I would be grateful if you could review the PR.

- add params for `assay` `slot` and `prefix` in `get_abundance_sc_wide()`
- make `get_abundance_sc_long()` handle `assay` and `slot` specification
- add arguments and params for `assay` `slot` in `get_abundance_sc_long()`
- add params for `assay` `slot` and `...` in `join_features()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8daf535ee183`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.