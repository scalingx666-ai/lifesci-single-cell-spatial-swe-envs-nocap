# Issue

**Title:** fix(fit_bulk): decompose the bulk only on genes with >= 10 counts, as R does

## Description

R spacexr's `fitBulk` (`prepareBulkData`) decomposes the bulk only on genes with at least 10 total counts across the tissue (`MIN_OBS = 10`, hard-coded), then renormalises every bulk gene in `get_norm_ref`. `fit_bulk` decomposed on all bulk genes.

Imaging panels have almost no such genes, so the existing Xenium/CosMx/Atera concordance was unaffected (99.7-100%). Sparse sequencing data has many: on StrataMap breast the extra genes moved the bulk proportions by up to 7 points (keratinocyte 33.3% vs R's 26.1%), and every cell was then fitted against shifted profiles.

Found by diffing R and rctd-py intermediates stage by stage on StrataMap: UMI-filtered cells, gene lists, reference profiles and sigma were identical; bulk proportions were the first thing to differ.

Agreement with R spacexr 2.2.1 doublet calls (same inputs, K=40 breast reference):

| Dataset | spot_class before | after |
|---|---:|---:|
| StrataMap breast (21,425 cells) | 80.7% | 99.5% |
| Visium HD breast, segmented cells (38,990) | 85.9% | 100% |
| Visium v1 breast (3,798 spots) | 91.5% | 100% |

Bulk proportions now match R to 1e-7. `tests/test_normalize.py::test_fit_bulk_drops_genes_below_min_obs` fails on main and passes here; full suite passes locally (152 passed).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1af2153e6b30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.