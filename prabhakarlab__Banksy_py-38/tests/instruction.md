# Issue

**Title:** Fix numpy 2.x incompatibility: remove <2.0 upper bound constraint

## Description

## Summary

- Remove the `<2.0` upper bound on the `numpy` dependency in `pyproject.toml` (`numpy>=1.21,<2.0` → `numpy>=1.21`)
- Bump version `1.3.4` → `1.3.5`
- Add `test_with_real_data.py`: end-to-end integration test using the bundled STARmap dataset

## Problem

Installing `pybanksy` 1.3.4 with a modern Python environment fails with:

```
pybanksy 1.3.4 requires numpy<2.0,>=1.21, but you have numpy 2.x which is incompatible.
```

numpy 2.0 was released in June 2024 and is now the default in many environments (conda-forge, pip, Google Colab, etc.). The hard `<2.0` cap makes the package uninstallable in these environments without manual pinning.

## Root cause & fix

The `<2.0` cap was a precautionary guard. A full audit of all source files in `src/banksy/` and `src/banksy_utils/` shows **zero incompatible numpy API usage**:

| Category | Status |
|---|---|
| Removed type aliases (`np.bool`, `np.int`, `np.float`, …) | ✅ None used |
| Removed functions (`np.in1d`, `np.row_stack`, `np.cumproduct`, …) | ✅ None used |
| Dtype usage | ✅ Explicit bitwidth types only (`np.int32`, `np.float64`, …) |
| Random API | ✅ Uses modern `np.random.default_rng()` |
| `np.matrix` check in `zscore()` | ✅ Still valid — `np.matrix` exists in numpy 2.x (deprecated, not removed); `scipy.sparse.mean()` still returns `np.matrix` |

The only change required is removing the version cap.

## Testing

End-to-end test with the bundled STARmap dataset (1207 cells × 1020 genes) under **numpy 2.3.5 / scipy 1.16.3**:

```
[PASS] Step 1: Load STARmap h5ad data           (shape: 1207 × 1020)
[PASS] Step 2: Initialize BANKSY                (spatial graph + AGF, 0.1s)
[PASS] Step 3: PCA + Leiden clustering          (7 clusters, ARI = 0.714, 1.6s)
[PASS] Step 4: Refine clusters                  (refined ARI = 0.723, 0.2s)
[PASS] Step 5: Verify label arrays & ARI values
ALL STEPS PASSED — numpy 2.3.5 is fully compatible
```

The test script `test_with_real_data.py` can be run from the repo root:

```bash
python test_with_real_data.py
```

## Checklist

- [x] No existing functionality changed
- [x] All numpy API usage audited across all source files
- [x] Full pipeline tested with real data under numpy 2.3.5
- [x] Backwards compatible (still supports numpy ≥ 1.21)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43e2d692db67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.