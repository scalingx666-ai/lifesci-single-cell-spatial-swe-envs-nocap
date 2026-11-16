# Issue

**Title:** fix(single): handle duplicate genes in CellPhoneDB scoring

## Description

## Background

`ov.single.run_cellphonedb_v5()` can fail during interaction scoring with the official CellPhoneDB EVT tutorial data when `score_interactions=True`:

```text
DuplicateError: Expected unique column names, got:
- 'NRXN1' 2 times
```

The official `normalised_log_counts.h5ad` input already has unique `var_names` and contains a single `NRXN1` entry. The duplication is introduced by CellPhoneDB's database mapping: one HGNC symbol can map to multiple protein records. After CellPhoneDB maps protein IDs back to gene symbols, its scoring matrix contains two `NRXN1` rows. Transposing that matrix creates duplicate columns, which newer dataframe consumers reject.

## Changes

- Collapse duplicate gene rows created by CellPhoneDB's protein-to-gene mapping before the official scaling and scoring steps.
- Average records expanded from the same input gene while preserving their original order. In the official EVT case, both `NRXN1` rows contain identical expression values, so the expression signal is unchanged and both database protein interaction records remain available.
- Apply the compatibility layer to both `cellphonedb_v5()` and `run_cellphonedb_v5()`.
- Restore the original CellPhoneDB function after both successful and failed analyses so the compatibility patch cannot leak into later calls.
- Add regression coverage for duplicate-gene collapsing and restoration after an exception.

## Validation

- `8 passed` across:
  - `tests/single/test_cpdb_scoring_compat.py`
  - `tests/single/test_comm_adapter.py`
  - `tests/architecture/test_optional_torch_dependencies.py`
- `compileall` passed.
- The new test file passed `flake8`; `git diff --check` passed.
- Completed a real analysis using the EVT dataset from CellPhoneDB's official `data_tutorial.zip`:
  - input: `1065 cells x 30800 genes`
  - after filtering: `19642 genes`
  - `100` permutations and `196` cell-type pairs
  - generated `interaction_scores (1441, 209)`
  - generated communication AnnData `(196, 1441)`

Official test data: https://github.com/ventolab/CellphoneDB/blob/master/notebooks/data_tutorial.zip

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7065d938595`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.