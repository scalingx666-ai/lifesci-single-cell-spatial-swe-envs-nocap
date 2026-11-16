# Issue

**Title:** Fix intermediate snapshot recording and query histories

## Description

##### Issue

Intermediate histories currently fail for normal documented configurations on master `2e7237a`:

```python
model = pacmap.PaCMAP(num_iters=(100, 100, 300), intermediate=True)
model.fit_transform(X)  # IndexError after the default final snapshot at step 450
```

LocalMAP fails the same way. A history request starting after step 0 also leaves its cursor uninitialized. Separately, `transform(..., intermediate=True)` attempts to store the fitted basis plus query points in a query-sized output array; 50 fitted Iris rows plus 4 query rows produces a `(54, 2)` into `(4, 2)` broadcast error.

##### Description of changes

- Initialize the history cursor independently of whether step 0 is requested, and stop recording once all requested snapshots are filled while allowing optimization to continue.
- Record only query rows during `transform`, preserving the allocated `(n_snapshots, n_query, n_components)` contract. Remove its hard-coded thirteen-snapshot cursor cap.
- Validate enabled history requests as nonempty, strictly increasing integer steps within the optimization budget. Invalid requests now raise `ValueError` instead of crashing later or returning unwritten slots. Disabled histories keep ignoring snapshot settings.
- Correct the README's history axis order and document the step constraints. For shorter runs, callers should explicitly provide snapshot steps within that run.

Optimization equations, pair sampling, seeds, and no-history outputs are unchanged. Tests compare selected snapshots against complete histories, and final embeddings/projections against no-history runs, using exact array comparisons.

##### Validation

Windows CPU, Python 3.12.14 / Numba 0.68.0 / NumPy 2.5.4 / pandas 2.3.3, `NUMBA_NUM_THREADS=2`, `OMP_NUM_THREADS=1`, `MKL_NUM_THREADS=1`:

- New tests on unchanged master: **18 failed, 1 passed**.
- With this change: **19 passed**, including real Iris fitting/projection, both estimators, snapshots without step 0, optimization past step 450, more than thirteen query snapshots, and invalid requests.
- Numba 0.57.1 / NumPy 1.24.4 / Python 3.11.16: **19 passed**.
- Entire standalone suite: **108 passed, 1 failed**. The existing Voyager Windows save/load failure is independently reproducible on master and fixed separately in #144; no test was disabled here.
- Private local integration of this change with #143 and #144: **126 passed** in the entire suite (102.24 seconds). Release notes and adjacent helper insertions required text conflict resolution, retaining all helper bodies unchanged. This is local combined evidence, not standalone head CI.

Linux, GPU and embedding-quality/performance improvements were not tested or claimed. Dependency files and CI are unchanged. The standalone suite used pandas 2.3.3 locally; the separate Python 3.13 CI failure and its remaining verification limits are recorded below.

##### Includes

- [x] Code changes
- [x] Tests
- [x] Documentation and release notes

##### AI disclosure

Prepared, tested, committed and submitted autonomously by OpenAI Codex, without independent human review. These are reproduced public API workflows on real Iris data, not a claimed personal production incident for the account holder. This branch is based directly on master, independently of #143/#144.

### Python 3.13 CI dependency alignment

The previous Python 3.13 OpenML setup failure was reproduced using the unchanged base `2e7237a` dataset loader with scikit-learn 1.8.0 and pandas 3.1.0, before entering PaCMAP's feature code. The parser passes an integer category to `re.search`. The local reproduction used Windows/Python 3.13.15; the failing CI used Ubuntu/Python 3.13.16.

`uv.lock` already locks pandas to 3.0.0, but the separate Python 3.13 requirements file allowed `pandas>=1.0` and installed 3.1.0. This commit aligns that test-only file with the existing lock. It does not change the runtime requirements, datasets, parser, tests, skips, backend installations, or CI matrix.

Local Python 3.13 validation with that requirements file and pandas 3.0.0: **56 passed, 30 Annoy cases deselected** (`pytest test/ -k "not annoy"`). Annoy and Voyager were not installed in this isolated environment, so this is partial local coverage, not a full CI pass. The unchanged OpenML fixtures loaded successfully. The full CI continues installing both optional backends.

Fresh current-head remote checks are pending; the previous Python 3.8–3.12 passes belong to the previous head.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e7237aa1d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.