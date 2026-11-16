# Issue

**Title:** fix(pp): avoid ARPACK int32 segfault in UMAP spectral init for ~1.66M–2M cells

## Description

.

## Root cause
`ov.pp.umap` (classic CPU path) calls umap-learn's `simplicial_set_embedding`, whose spectral init uses `scipy.sparse.linalg.eigsh` with `ncv = int(sqrt(n))` for graphs **below 2M nodes** (lobpcg only from 2M).

scipy ≥ 1.17 replaced Fortran ARPACK with a C port (`arnaud`) that indexes the Lanczos basis as `&v[ldv*j]` with `int ldv` (see `arnaud_s_double.c`, e.g. `dcopy_(&n, resid, &int1, &v[ldv*(V->aitr_j)], &int1)`). Once `n * j > 2**31 - 1` the offset wraps negative and OpenBLAS `dcopy_` writes to unmapped memory → `segfault ... error 6 in libscipy_openblas`. With `ncv ≈ sqrt(n)` this happens from **~1.66M cells** up to 2M — the reporter has 1,829,054 cells.

Verification:
- 1.7M-node 15-NN graph, `umap.spectral._spectral_layout`:
  - scipy 1.16.3 (Fortran ARPACK, 64-bit addressing): eigsh finishes (870 s), no crash. So the bug only shows up with the 1.17 C port.
  - Same graph with `method='lobpcg'`: finite embedding in 89 s.
- I could not run the scipy 1.17 wheels on our CentOS 7 / glibc 2.17 node. The diagnosis comes from reading the scipy 1.17.1 source, and it matches the reporter's crash signature.

## Fix
- Add a narrow context manager around the classic `simplicial_set_embedding` call.
- It sets `method='lobpcg'` (umap's own large-graph solver) only when `n * ncv` would exceed int32 and no method was given.
- It covers single-component and per-component (`multi_component_layout`) spectral init.
- Smaller graphs are untouched: the embedding is bit-identical (tested).
- A one-line note is printed when the switch happens.

## Tests
`tests/pp/test_umap_large_spectral_init.py` (5 tests):
- threshold check
- lobpcg is forced only above the threshold
- an explicit method is respected
- the patch is restored on exit
- small-graph output is unchanged

Workaround for users on older omicverse: `ov.pp.umap(adata, init_pos='random')` or `method='umap-gpu'`, or pin `scipy<1.17`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VVqVNig3oV6wz42YiQ9obZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db7be141626b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.