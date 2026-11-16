# Issue

**Title:** Use seed zero for permutation shuffling

## Description

The accepted seed `0` currently bypasses `_ridx` shuffling because the helper checks `if seed:`. It returns repeated identity permutations, while GSEA and WAGGR still perform permutation-based inference. This patch checks `seed is not None`, allowing zero to choose its normal seeded stream and retaining the internal None identity sentinel.

Minimal reproduction on upstream d0260c3e0bbc0d2f9882eddd3db872799004df99:

```python
import numpy as np
from decoupler.mt._gsea import _ridx
actual = _ridx(times=100, nvar=20, seed=0)
expected = np.tile(np.arange(20), (100, 1))
rng = np.random.default_rng(0)
for row in expected:
    rng.shuffle(row)
np.testing.assert_array_equal(actual, expected)
```

Before the patch, `actual` contains only identity rows. After it, the complete matrix matches the explicit NumPy reference. Added tests cover zero and the default 42, deterministic repeated calls, and the internal None sentinel. Public None remains subject to the existing input-validation contract.

Validation against complete current source: the GSEA/WAGGR test files give one failure and 17 passes before the correction, and all 18 pass after it. Changed source/tests pass Ruff lint and formatting checks. Initial collection needed package metadata and the existing GSEApy test dependency; these were supplied before the recorded scientific test runs. The full package suite was not run.

The already-published released-2.2.0 reproduction also tests both public APIs using the package toy data (30 observations, 20 features, five sources, 1,000 permutations). Correcting seed zero changes adjusted-p<0.05 counts from 0 to 40 for GSEA and 150 to 58 for WAGGR; complete seed-42 output files remain unchanged in that recorded run. These are changed calls, not established false-positive/false-negative counts. No affected published conclusion or broad validation of all inference formulas is claimed.

Report, runnable released-package reproductions, before/after outputs and evidence archive: https://cheerfulduck.com/research/audits/decoupler-zero-seed-permutations . Bounded searches did not find an exact prior report. Prepared with AI assistance; independent human scientific review and a released fix are not claimed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0260c3e0bbc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.