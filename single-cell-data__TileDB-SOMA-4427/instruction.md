# Issue

**Title:** [r] Remove internal forwarding of deprecated `tiledbsoma_ctx`

## Description

**Issue and/or context:**

Addresses [SOMA-832](https://linear.app/tiledb/issue/SOMA-832/r-remove-all-internal-usage-of-deprecated-tiledbsoma_ctx)

PR #4355 introduced `SOMAContext` and deprecated `tiledbsoma_ctx` / `SOMATileDBContext`. In this transition period user-facing functions accept `tiledbsoma_ctx`, call `get_soma_context()` to resolve it into a `SOMAContext`, and throw a deprecation warning. However, after resolution some functions were still forwarding the original `tiledbsoma_ctx` value to downstream internal calls. 

**Changes:**

- `Factory.R`: Removed `tiledbsoma_ctx = tiledbsoma_ctx` from all 12 `$new()` constructor calls (the resolved `context` is already being passed)
- `SOMAOpen.R`: Removed `tiledbsoma_ctx = tiledbsoma_ctx` from 6 factory `Open` calls (context already resolved by `get_soma_context()` at the top of `SOMAOpen()`)
- `datasets.R`: Removed `tiledbsoma_ctx = tiledbsoma_ctx` from 2 factory calls in `load_dataset()` (same pattern)
- `write_seurat.R`: Removed `tiledbsoma_ctx = tiledbsoma_ctx` from 8 internal calls within `write_soma.Seurat()` (context already resolved at function entry)

**What was not changed:**

- Exported functions still accept `tiledbsoma_ctx` (deprecation policy requires keeping it until defunct)
- `SOMAObject` still stores `private$.tiledbsoma_ctx` and the `$tiledbsoma_ctx` active binding still works

**Notes for reviewers:**

- Verified all remote tests (cloud/carrara) still pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4de5c736f0b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.