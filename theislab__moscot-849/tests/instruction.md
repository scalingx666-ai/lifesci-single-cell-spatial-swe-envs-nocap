# Issue

**Title:** fix: restore the test suite on Python 3.12 (pandas 3, anndata 0.13)

## Description

The `Test` workflow is red on `main` for both 3.12 legs and has been since mid-June — the [scheduled run of 2026-08-15](https://github.com/theislab/moscot/actions/runs/31866113426) reports `27 failed, 732 passed` identically on ubuntu and macOS. The 3.11 leg stays green because it resolves older anndata/pandas. Two unrelated breakages, both dependency drift:

## 1. Positional indexing of a `pandas.Series` (24 failures)

`src/moscot/base/problems/_mixins.py:288` and `:312`:

```python
v = np.array(tm_batch.argmax(0))
out.extend(source_df[annotation_label][v[i]] for i in range(len(v)))
```

`v` holds **positions**, while `source_df[annotation_label]` is a Series indexed by observation names. `series[np.int64(0)]` therefore relied on pandas' positional fallback for non-integer indexes, which pandas 2 deprecated and **pandas 3 removed**:

```
E   KeyError: np.int64(0)
pandas/_libs/index.pyx:583: KeyError
```

Every `test_annotation_mapping` case (`mapping_mode="max"`, across the space, time and cross-modality mixins) hits this. Fixed with `.iloc`, which is exactly what the fallback used to do — so the behaviour is unchanged on older pandas too.

This one is a genuine bug in moscot rather than a test artefact: any user calling `annotation_mapping(..., mapping_mode="max")` on pandas 3 gets the same `KeyError`.

## 2. `AnnData.concatenate` was removed (3 failures)

`tests/problems/base/test_general_problem.py` used the long-deprecated method, giving `AttributeError: 'AnnData' object has no attribute 'concatenate'` in the three `test_set_graph_xy` cases. Replaced with `anndata.concat([...])`.

## Verification

Full suite on Python 3.12 with anndata 0.13.2 and pandas 3.0.5: **759 passed, 1 skipped, 0 failed** (was 732 passed / 27 failed — exactly the 27 restored). `black`, `isort`, `ruff` clean.

Independent of #848 (lint) and #846 (sparsify); together the three take CI back to green.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7a0567973d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.