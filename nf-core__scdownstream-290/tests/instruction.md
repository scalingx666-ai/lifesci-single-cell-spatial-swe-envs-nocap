# Issue

**Title:** Fix CELLBENDER_MERGE for 10x Flex gene-set mismatch

## Description

## Summary

- Fix `CELLBENDER_MERGE` failing on 10x Flex data where filtered and raw matrices have different gene sets ()
- Subset CellBender output to both filtered barcodes and genes before writing the ambient-corrected layer
- Formalize the change as an nf-core modules patch (`cellbender-merge.diff`) so it survives future module updates

## Test plan

- [x] `nft subworkflows/local/ambient_correction/tests/main.nf.test` — all 12 tests pass, including both cellbender cases; no snapshot changes
- [x] Manual validation on 10x Flex data with `ambient_correction = 'cellbender'`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e302f37d006`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.