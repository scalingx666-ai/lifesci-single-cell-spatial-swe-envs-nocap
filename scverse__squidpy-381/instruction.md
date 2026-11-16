# Issue

**Title:** Delaunay optimization

## Description

### Types of changes
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [ ] New feature (non-breaking change which adds functionality)

### Description
In the computation of the spatial graph from the Delaunay triangulation, the code to obtain the list of rows and columns is unnecessary given that they are already computed by `scipy.spatial.Delaunay` and thus stored into `tri.vertex_neighbor_vertices`.
The connections are already in a format suitable for the csr_matrix.

Since the building of the csr_matrix between the two methods (delaunay vs. nearest neighbor) is now different I replaced the way of setting the diagonal elements in the case of `set_diag=True` into a way that is independent of how the matrix is built.

The modification results in a speed-up of the `gr.spatial_neighbors` function from:
`928 ms ± 9.53 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)`

to
`46 ms ± 2.28 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)`

on the `sq.datasets.visium_fluo_adata` dataset with 2800 observations.

### How has this been tested?
The modifications replace an existing piece of code without adding functionalities and the previous version didn't actually contain a bug, so I only run the `test_spatial_connectivity.py` test.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `442a952a6eb0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.