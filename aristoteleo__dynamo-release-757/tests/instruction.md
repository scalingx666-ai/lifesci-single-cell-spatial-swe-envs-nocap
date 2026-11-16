# Issue

**Title:** Store ss_estimation count layers as CSR (~10x faster steady-state fit, bit-identical)

## Description

## TL;DR
The default single-core steady-state RNA-velocity estimation is ~10× slower than it should be — **not** because of missing parallelism, but because the count layers are **CSC** and the fit indexes one gene-row at a time (`data[i]`), which is `O(total nnz)` for CSC. Storing them as **CSR** makes row indexing `O(row nnz)`: **9–10× faster**, **bit-for-bit identical** results, portable, no multiprocessing.

This supersedes **#499** (evaluated below).

## Profiling (default `dyn.tl.dynamics(cores=1)`, deterministic, warm)
```
32.27s  ss_estimation.fit
31.67s    scipy/sparse/_index.py:__getitem__   (4018 calls)   <-- U[i] / S[i]
30.68s      scipy/sparse/_csc.py:_get_intXslice                <-- CSC row slicing
 1.47s    fit_gamma_steady_state               (2000 calls)   <-- actual fit math
```
Microbenchmark of the same 2,000-gene fit: CSC `U[i]` indexing 15.2s vs **CSR 0.40s (38×)**; the per-gene math is <1s and threads/process-pools barely help (numpy already releases the GIL).

## Fix
```python
# ss_estimation.__init__, after building self.data
for _key, _val in self.data.items():
    if _val is not None and issparse(_val) and not isinstance(_val, csr_matrix):
        self.data[_key] = _val.tocsr()
```

## Results — `master` vs this PR (warm, end-to-end)
| model | cores | master | this PR | speedup |
|---|---|---|---|---|
| deterministic | 1 | 34.73s | **3.61s** | **9.6×** |
| stochastic | 1 | 63.91s | **6.43s** | **9.9×** |

`cores=1` now matches the old `cores=4`; timing is flat across cores (the fit is no longer the bottleneck).

## Numerical equivalence — bit-exact (max|Δ| = 0)
`vel_params` (all 19 kinetic params) and `velocity_S`/`velocity_N` are identical to `master` on:
- conventional **deterministic** and **stochastic** (pancreas), and
- the **metabolic-labeling** path (neuron `new`/`total`).

Adds `tests/test_tl.py::test_ss_estimation_stores_csr`.

## Why this instead of #499
PR #499 (`ss estimate refactor`) replaced the fit with a `multiprocessing` pool. Tested on current master it **crashes on every path** (`AttributeError: 'csr_matrix' object has no attribute 'A'` — a scipy attribute removed years ago — plus an argument mis-alignment), and uses `mp.get_context("fork")` (Linux-only). It also targets the wrong bottleneck: the work is <1s once the data layout is fixed, so its apparent "10× from 2 cores" is an artifact of iterating `zip(U, …)` rather than real parallel scaling. This PR fixes the actual root cause with a one-line, zero-risk, bit-identical change that helps the default path everyone uses.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8af4076bd64a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.