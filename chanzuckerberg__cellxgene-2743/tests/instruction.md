# Issue

**Title:** fix: improve anndata error msg

## Description

#### Reviewers
**Functional:** 

**Readability:** 

---

## Changes

* **Modify** `server/data_anndata/anndata_adaptor.py` to improve error handling during `.h5ad` file loading.
* **Add** a specific check for `anndata` forward-compatibility errors (e.g., `IORegistryError`) within the `_load_data` exception block.
* **Modify** the generic "File not found or is inaccessible" error message to provide actionable feedback when a version mismatch is detected.

---

## Context & Motivation

Currently, when `cellxgene` attempts to load an `.h5ad` file created with a newer version of `anndata` than the one installed in the server environment, it triggers an `anndata._io.specs.registry.IORegistryError`. This frequently occurs with files created in `anndata` **v0.12.0+**, which utilizes a new `null` encoding for `None` types (which is found in `uns['log1p']` resulting from scanpy's `sc.pp.log1p()` function).

In these cases, the `AnndataAdaptor` catches the generic exception and reports that the file is "not found or is inaccessible." This is misleading, as the file exists and permissions are correct; the issue is an environment mismatch.

This change catches errors containing `"No read method registered"` and `"IOSpec"`, providing the user with the actual internal error and a suggestion to upgrade their environment.

## Testing

1. **Created a "Broken" Environment:** Python 3.10 with `anndata==0.11.4`.
2. **Generated a Test File:** Used `anndata==0.12.2` to save a file containing `adata.uns['log1p'] = {'base': None}` from running `sc.pp.log1p(adata)`.
3. **Verified the Fix:**
* **Before:** `cellxgene launch` reported "File not found or is inaccessible."
* **After:** `cellxgene launch` correctly identified the version mismatch and suggested `pip install --upgrade anndata`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fddcd042ac5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.