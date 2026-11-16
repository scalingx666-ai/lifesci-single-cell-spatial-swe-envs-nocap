# Issue

**Title:** fix(pl): plotting fixes from the 0.7.0 review

## Description

Summary: The second of three PRs with fixes from the review of the 0.7.0 refactor. This one covers the plotting functions.

Changes:
- The legacy heatmap passes scanpy an AnnData instead of a view.
- Chromosome heatmaps save the way scanpy's `savefig_or_show` does.
- `pl.spatial_cnv` saves the figure once and draws the tissue the way `sc.pl.spatial` does.
- The fast heatmap dendrogram and `standard_scale='var'` now match the legacy output.
- The heatmap dendrogram is computed from the window covariance on every call and stored in `uns`, and the docs describe how. scanpy no longer warns about a PCA fallback.
- Group labels are thinned with matplotlib's `FixedFormatter` instead of custom code.

Testing: the full test suite passes on the cluster (679 passed, 12 skipped).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea800d5483ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.