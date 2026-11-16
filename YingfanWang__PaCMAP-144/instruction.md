# Issue

**Title:** Fix loading saved Voyager indexes on Windows

## Description

##### Issue

Fix Windows round trips of saved Voyager-backed PaCMAP/LocalMAP estimators. The existing `test_pacmap_mnist[voyager]` fails on unchanged master `2e7237a`: `pacmap.load(...)` reports a corrupted/unsupported index even though PaCMAP just saved it.

##### Description of changes

On Windows, `attach_index` now opens the Voyager index in `rb` mode and passes the binary file object to `voyager.Index.load`. Other platforms retain the native path reader. The file is closed after loading; the restored index remains usable for queries and projection.

A standalone Voyager 2.2.2 probe isolated the read path: native-path and binary-stream saves produced identical 29,747-byte files. Native path loading failed on both; binary-file loading succeeded on both, with identical neighbor IDs and zero distance difference from the original index. No file-format conversion, index rebuilding, or change to Annoy/FAISS is involved.

Four regression cases fit real Iris data using PaCMAP/LocalMAP, save the estimator, load through either common-prefix or explicit-path APIs, compare saved/restored queries and embeddings, then project new points after the file has closed. These cases require the optional Voyager dependency; all four executed locally without skips.

Validation on Windows CPU (`NUMBA_NUM_THREADS=2`, `OMP_NUM_THREADS=1`, `MKL_NUM_THREADS=1`):

- Unchanged master: existing MNIST Voyager round-trip test fails; all four new regression cases fail at index loading.

- With this fix: **94 passed** in the complete `test/` suite, including existing Annoy/FAISS/Voyager and MNIST/Fashion-MNIST tests (97.80 seconds).

- Voyager 2.0.0 / Numba 0.57.1 / NumPy 1.24.4 / Python 3.11.16: **4 passed**.

- Full-suite environment: Voyager 2.2.2 / Numba 0.68.0 / NumPy 2.5.4 / scikit-learn 1.9.1 / pandas 2.3.3 / Python 3.12.14. pandas 2.3.3 was installed locally to avoid a separate pandas 3.1.0/OpenML parsing error; repository dependency and CI files are unchanged.

- `git diff --check` passes. Linux and performance were not tested locally. Voyager's Python file-object API holds the GIL during loading; the native reader remains unchanged outside Windows.

This branch is based directly on master and is independent of #143; its 94-test result does not include #143's new worker-limit tests.

##### Includes

- [x] Code changes

- [x] Tests

- [x] Release notes

### Combined local validation

The independent changes in #143, #144 and #145 were combined in a private local branch: the complete suite passed **126 tests** on Windows CPU. Release notes and adjacent helper insertions needed conflict resolution; both original helper bodies were preserved. The branch was not pushed. A real Iris fit → save → load → transform workflow retained `numba_threads=1` and restored the caller mask to 2. A sequential fit in a single Python worker thread restored that worker's previous mask and left the main-thread mask unchanged. This is local integration evidence, not standalone head CI, a performance benchmark, or a test of concurrent fits.

### AI disclosure

Prepared, tested, committed and submitted autonomously by OpenAI Codex, without independent human review. The failure was found while running this repository's existing save/load test; I am not claiming a personal production incident for the account holder.

### Python 3.13 CI dependency alignment

The previous Python 3.13 OpenML setup failure was reproduced using the unchanged base `2e7237a` dataset loader with scikit-learn 1.8.0 and pandas 3.1.0, before entering PaCMAP's feature code. The parser passes an integer category to `re.search`. The local reproduction used Windows/Python 3.13.15; the failing CI used Ubuntu/Python 3.13.16.

`uv.lock` already locks pandas to 3.0.0, but the separate Python 3.13 requirements file allowed `pandas>=1.0` and installed 3.1.0. This commit aligns that test-only file with the existing lock. It does not change the runtime requirements, datasets, parser, tests, skips, backend installations, or CI matrix.

Local Python 3.13 validation with that requirements file and pandas 3.0.0: **37 passed, 4 skipped, 30 Annoy cases deselected** (`pytest test/ -k "not annoy"`). Annoy and Voyager were not installed in this isolated environment, so this is partial local coverage, not a full CI pass. The unchanged OpenML fixtures loaded successfully. The full CI continues installing both optional backends.

Fresh current-head remote checks are pending; the previous Python 3.8–3.12 passes belong to the previous head.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e7237aa1d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.