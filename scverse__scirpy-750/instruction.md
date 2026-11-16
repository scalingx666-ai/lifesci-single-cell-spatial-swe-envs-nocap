# Issue

**Title:** Fix deprecated AnnData coordinate-key checks in clonotype networks

## Description

Plotting a clonotype network and exporting its layout to igraph emit an AnnData `obsm_keys()` FutureWarning. Check membership directly in `adata.obsm` in both paths, preserving the existing missing-coordinate errors.

Related to #731; this addresses one warning class and leaves other warnings visible.

The existing plotting and igraph tests now treat this specific warning as an error. The igraph tests retain their node-count and coordinate assertions and cover a custom basis. Additional tests check the missing-coordinate error for both APIs with AnnData and MuData and default and custom bases.

Validation on Windows with Python 3.12.14 and AnnData 0.13.3.post0:

- The same 140 regression cases fail on the original source with the `obsm_keys` FutureWarning and pass on the fixed source, with no skips. Both runs use the same interpreter and byte-identical test files.
- The full clonotype and plotting modules report 272 passed and 4 strict XPASS results. Those four cases also produce strict XPASS on the original source: their existing Windows xfail marks expect an igraph coordinate issue, but the assertions pass in this environment. No xfail settings were changed.
- `pip check`, Ruff lint/format checks on the changed Python files, and `git diff --check` pass.
- The full repository suite and Linux/Python version matrix were not run locally.

- [x] CHANGELOG.md updated
- [x] Regression tests added

No tutorial update is needed for this compatibility fix.

Implementation and test preparation were assisted by AI. The before/after test runs and baseline failure messages were checked explicitly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06f8c7e6c1ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.