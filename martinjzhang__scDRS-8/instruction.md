# Issue

**Title:** Updated cli

## Description

### An updated command line interface with functionality
- Compute scores: `scdrs compute-score`. This perform the same function as python compute_score.py
- Downstream analyses: `scdrs perform-downstream`, which perform the same function as python compute_downstream.py
- Munge .gs file: `scdrs munge-gs`, which takes a gene set score file such as MAGMA association z-scores (or p-values) and format to the scdrs .gs format

The downstream analyses now only handle either one of the (1) group analysis (2) correlation analysis (3) gene analysis rather than performing all at once as in `python compute_downstream.py`. I think this way is cleaner.

The existing files are not changed to ensure the compatibility.

### Several utility functions are moved from cli script to `scdrs.util` module as these can be also reused in python API.
- `scdrs.util.convert_species_name`: taken from python compute_score.py
- `scdrs.util.load_h5ad`: Load h5ad file and optionally filter out cells and perform normalization
- `scdrs.util.load_drs_score`: Load drs scores, could be multiple score files, depend on the `score_path` parameter pattern. Either it is path to a single score file, such as /path/to/trait.full_score.gz  or a file pattern for multiple score files, such as /path/to/@.full_score.gz
- `scdrs.util.downstream_group_analysis`: Perform the group-level downstream analysis for scDRS results
- `scdrs.util.downstream_corr_analysis`: Perform the correlation between cell-level variables with scDRS scores
- `scdrs.util.downstream_gene_analysis`: Perform the correlation between gene-level variables with scDRS scores

### Discussion points
1. Whether to move the downstream code to scdrs.method
2. Better names on the functions.
3. Any other suggestions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa5121f7c091`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.