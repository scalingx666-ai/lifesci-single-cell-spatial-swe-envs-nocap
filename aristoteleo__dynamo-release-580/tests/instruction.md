# Issue

**Title:** Debug h5ad saving

## Description

Some parts of adata still have incompatible data types. Including:

- [x] fate output -> convert to a different format when saving, convert back when loading
- [x] kmc object -> convert to a different format when saving, convert back when loading
- [x] umap object -> now umap object will not be saved, it will be constructed with parameters when needed.
- [x] velocity parameters -> convert to compatible data type
- [x] cell phase genes -> convert to compatible data type
- [x] init cells -> convert to compatible data type
- [x] fixed points and nullclines  -> convert to compatible data type, nullclines are replaced by `NCx` and `NCy`

In the future, we will use `import_h5ad` and `export_h5ad` for saving and loading processed data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5e9017f84ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.