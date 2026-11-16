# Issue

**Title:** Speed up neighbors for large datasets and fix IVF searches beyond 2**32 query values

## Description

- all_neighbors: overlap factor 2 for clusters of >= 20,000 cells, also with explicit n_clusters
- free the representation before computing connectivities
- convert graphs with > 2**31 entries to SciPy CSR on the GPU
- ivfflat/ivfpq: search in batches of < 2**31 query values (cuVS IVF-Flat returns wrong neighbors for queries beyond the 2**32nd value of one query matrix)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c4b6dc9d944`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.