# Issue

**Title:** fix: get CI green under pandas 3.1; adopt anndata.acc; document PETSc UCX log flood

## Description

Part of #1389. .

## Bug fixes
- **CI on `main`:** `test_bare_string_does_not_warn` and `test_trends_gene_layer_signal_no_warning` turned every `DeprecationWarning` into an error. anndata 0.13.4 sets a pandas option that pandas 3.1 deprecates, emitting `Pandas4Warning` (fixed in scverse/anndata#2671, not yet released). The tests now escalate only CellRank's own "will be deprecated in CellRank" warnings, which is what they check.
- `cr.pl.log_odds(..., layer="X")` raised `KeyError` for gene keys without a `threshold`.

## Changes
- Gene vectors are read with `anndata.acc` instead of the deprecated `AnnData.obs_vector`. **Requires `anndata>=0.13`** (was `>=0.11`).
- `pd.merge(..., copy=)` dropped; the keyword is deprecated under copy-on-write.
- Installation docs: a troubleshooting section for the UCX error flood with conda-forge PETSc on InfiniBand nodes with a low `ulimit -l`, with the `UCX_TLS=self,sm,tcp` workaround.

Local: `hatch test -py 3.12`: 1143 passed, 102 skipped (PETSc/R). The PETSc job will still fail on the pyGPCCA `getVecs` issue until pygpcca 1.1.0 is used there (#1389).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94f2592f1b0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.