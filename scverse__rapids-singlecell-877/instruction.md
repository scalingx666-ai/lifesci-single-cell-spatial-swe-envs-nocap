# Issue

**Title:** Build the neighbors connectivities' CSR on the host at every size

## Description

`pp.neighbors` converted the UMAP connectivities to CSR with CuPy's `tocsr()` on the GPU whenever they had fewer than 2**31 entries. `tocsr()` sorts every entry, and its temporaries come on top of the kNN arrays and the COO graph still on the GPU, so graphs just below that limit ran out of memory: 75M cells with `n_neighbors=15` (1.87B entries) failed on a 96 GB GPU, while 100M cells (2.5B entries) worked because they took the host path.

cuML's graphs are already sorted by row and column, so `_large_coo_to_host_csr` (added in #825 for graphs from 2**31 entries on) only computes the row pointers on the GPU and builds the CSR on the host; it falls back to a host `tocsr()` if the entries are ever unsorted. It is now used for every COO graph. `gauss` and `jaccard` return CSR and are unchanged; `bbknn` keeps its GPU path because it trims on the GPU CSR.

- the connectivities are identical (`indptr`, `indices`, `data`) to the GPU `tocsr()` on 2M real cells (48M entries); `indptr` is now always int64
- `rsc.pp.neighbors(..., n_neighbors=15, algorithm="all_neighbors")` on 75M Tahoe-100M cells now completes
- `test_neighbors.py`, `test_mg_neighbors.py`, `test_wnn.py`, `test_spatial_neighbors*.py` pass

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `789a251daf8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.