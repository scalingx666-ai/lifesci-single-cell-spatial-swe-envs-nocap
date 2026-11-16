# Issue

**Title:** Allow per-estimator Numba worker limits

## Description

## Context of the PR

Related to #126: users currently have to configure `NUMBA_NUM_THREADS` outside the estimator to limit PaCMAP's Numba workers. Add an optional `numba_threads` parameter to PaCMAP and LocalMAP so this part of the CPU budget can be controlled per estimator.

This deliberately controls **Numba only**, not nearest-neighbor backends or BLAS/PCA. It does not introduce a general `n_jobs` promise or change the default worker mask.

## Contributions of the PR

- Apply a positive worker limit during `fit`, `fit_transform`, `transform`, and direct pair sampling, then restore the caller's previous Numba mask in `finally`.

- Preserve the existing setting when `numba_threads=None`, reject invalid values, and let Numba enforce its configured pool maximum. Old saved instances without the new attribute retain the default behavior.

- Document the scope and add focused tests using actual Iris fitting/projection, worker-mask observations, restoration after errors, invalid settings, and sklearn cloning. Both estimators are covered.

Numba implements these masks in thread-local storage: https://numba.readthedocs.io/en/stable/developer/threading_implementation.html#the-implementation . This does not add a guarantee that all existing PaCMAP/backend operations are safe to call concurrently.

### Validation

Windows CPU, `NUMBA_NUM_THREADS=2`, `OMP_NUM_THREADS=1`, `MKL_NUM_THREADS=1`:

- New tests on unchanged master `2e7237a`: **12 failed, 1 passed** (the parameter is unavailable).

- New tests with this change: **13 passed**, Python 3.12.14 / Numba 0.68.0 / NumPy 2.5.4.

- Minimum declared Numba line: **13 passed**, Python 3.11.16 / Numba 0.57.1 / NumPy 1.24.4 / scikit-learn 1.3.2 / FAISS 1.7.4.

- Existing offline tests plus new tests: **77 passed, 20 deselected**, with Annoy 1.17.3, FAISS 1.15.1 and Voyager 2.2.2 installed.

- Entire `test/` suite with pandas 2.3.3: **102 passed, 1 failed**. The failure is `test_pacmap_mnist[voyager]`, whose saved index fails to load on Windows. The same test fails on unchanged master with the same environment; no assertion or test was disabled. This PR does not change serialization.

A pandas 3.1.0 run failed earlier in sklearn's OpenML ARFF parsing, before estimator execution. The full result above uses pandas 2.3.3 installed only in the local environment; repository dependency files and CI are unchanged. Python 3.8 grammar and `git diff --check` pass. Linux, GPU, throughput, and concurrent-call behavior were not tested locally.

### Checks before merging PR

- [x] Added documentation for the new parameter

- [x] Added unit tests

- [x] Updated release notes

- [ ] Entire suite green locally (one independently reproduced baseline Voyager failure)

### Combined local validation

The independent changes in #143, #144 and #145 were combined in a private local branch: the complete suite passed **126 tests** on Windows CPU. Release notes and adjacent helper insertions needed conflict resolution; both original helper bodies were preserved. The branch was not pushed. A real Iris fit → save → load → transform workflow retained `numba_threads=1` and restored the caller mask to 2. A sequential fit in a single Python worker thread restored that worker's previous mask and left the main-thread mask unchanged. This is local integration evidence, not standalone head CI, a performance benchmark, or a test of concurrent fits.

### AI disclosure

Prepared, tested, committed and submitted autonomously by OpenAI Codex. There has been no independent human review. #126 is an existing user request; I am not claiming the account holder personally encountered this limitation in a production project.

### Python 3.13 CI dependency alignment

The previous Python 3.13 OpenML setup failure was reproduced using the unchanged base `2e7237a` dataset loader with scikit-learn 1.8.0 and pandas 3.1.0, before entering PaCMAP's feature code. The parser passes an integer category to `re.search`. The local reproduction used Windows/Python 3.13.15; the failing CI used Ubuntu/Python 3.13.16.

`uv.lock` already locks pandas to 3.0.0, but the separate Python 3.13 requirements file allowed `pandas>=1.0` and installed 3.1.0. This commit aligns that test-only file with the existing lock. It does not change the runtime requirements, datasets, parser, tests, skips, backend installations, or CI matrix.

Local Python 3.13 validation with that requirements file and pandas 3.0.0: **50 passed, 30 Annoy cases deselected** (`pytest test/ -k "not annoy"`). Annoy and Voyager were not installed in this isolated environment, so this is partial local coverage, not a full CI pass. The unchanged OpenML fixtures loaded successfully. The full CI continues installing both optional backends.

Fresh current-head remote checks are pending; the previous Python 3.8–3.12 passes belong to the previous head.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e7237aa1d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.