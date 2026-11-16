# Issue

**Title:** fix(cytotrace): handle None layer key in invalid-layer error message

## Description

## What

Fixes `tests/test_kernels.py::TestCytoTRACEKernel::test_layer[foo]` on the pre-release-deps job (anndata 0.13.0rc1).

## Why

anndata >=0.13 now includes `None` in `adata.layers.keys()` (it aliases `.X`). When an invalid layer is requested, CytoTRACE builds the `KeyError` message via:

```python
sorted({'X'} | set(self.adata.layers.keys()))
```

With `None` now present, sorting a `{str, None}` set raises `TypeError: '<' not supported between instances of 'str' and 'NoneType'` — so the test sees a `TypeError` instead of the expected `KeyError`.

## Fix

Drop `None` from the set before sorting (`"X"` already represents the main matrix in the message). Verified against anndata 0.13.0rc1 in the pre-release env — all `test_layer` params pass.

> Non-blocking job (`continue-on-error`); part of the pre-release-deps cleanup.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c079caeebd9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.