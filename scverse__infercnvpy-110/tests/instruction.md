# Issue

**Title:** Fix heatmap passing of uns data to scanpy.pl.heatmap

## Description

In `chromosome_heatmap`, remove unnecessary existence test and copying of `adata.uns[f"{groupby}_colors"]` to `tmp_adata.uns` (which was already defined to be equal to `adata.uns` in PR ).

In `chromosome_heatmap_summary`, set `tmp_adata.uns` equal to `adata.uns` at definition, just as in `chromosome_heatmap`, and remove unnecessary test, as above. This prevents `scanpy.pl.heatmap` from issuing a `dendrogram data not found` warning and recomputing dendrogram when `tmp_adata` is passed with `dendrogram=True`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83acb914fb17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.