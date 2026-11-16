# Issue

**Title:** fix: numba cache data files named by key, so concurrent compiles can't mix up signatures

## Description

Summary: When several processes compile different signatures of the same numba kernel at the same time against one on-disk cache, the cache can end up mapping one signature to another signature's machine code. Every later call with that signature then fails with "can't unbox array from PyObject", until the cache is deleted. This PR names each cached data file after its cache key, so a data file can only ever hold the code for its own key.

Background:
- The failure showed up twice when running the test suite with many pytest-xdist workers on the HMGU cluster. Users can hit it too, for example with several jobs on a shared environment on first use, or with process workers fed different dtypes.
- How it happens: numba's default index/data cache file picks the next free data file number from the index it has just read, writes the index, then the data file. Two processes that read the same index both pick the same number. If one process's index and the other's data file are the last to land, the index points to the wrong code.

Changes:
- `infercnvpy._numba` has a small `njit` helper: `numba.njit(nogil=True)` with a cache whose data files are named after a hash of the cache key. Each data file is written before the index.
  - A concurrent index write can still lose an entry, which costs one recompile, but it can no longer point to the wrong code.
- `njit_parallel` builds both twins with it, so it is still a parallel kernel on the main thread and a serial nogil twin elsewhere. The other cached kernels use it too.
- Caching stays on for users.
- The helper subclasses numba's cache classes (`IndexDataCacheFile`, `FunctionCache`), which are not public API.

Testing:
- New `tests/test_numba_cache.py` forces the bad write order between two loads of a kernel module in one subprocess, then calls the kernel with float32 and float64 in a fresh subprocess. It fails on main with the "can't unbox array" error and passes with this change.
- In a stress run on the cluster, 16 processes compiled one kernel for 4 dtypes into a shared cache dir. Main broke in 4 of 10 rounds, this branch in 0 of 10.
- The full suite passes on the cluster twice with 16 workers (482 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f06b64fb308`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.