# Issue

**Title:** Fix NaN pseudotime when a cell is far from every waypoint

## Description

## Problem

`_compute_pseudotime` weights each cell's waypoints by `exp(-0.5 * (d / sdv) ** 2)` and normalises the weights per cell. The bandwidth `sdv` shrinks as `(n_waypoints * n_cells) ** (-1/5)`, so in a large dataset a cell whose nearest waypoint is more than ~38.6 bandwidths away has every weight underflow to 0 in float64. Normalising gives 0 / 0 = NaN, and `pseudotime -= np.min(pseudotime)` then makes the pseudotime of every cell NaN; the refinement never converges, since the correlation is NaN.

With default arguments, terminal-state detection then fails. On palantir 1.4.5:

```python
import numpy as np
import pandas as pd
import palantir

data = pd.DataFrame(np.random.default_rng(0).normal(size=(50_000, 10)))
data.index = data.index.astype(str)
palantir.core.run_palantir(data, "0")
# ArpackError: ARPACK error -9: Starting vector is zero.
```

With this PR it runs, with no NaN in the pseudotime or the fate probabilities, with and without `scale_components`.

Up to 1.4.2, the pandas `sum` skipped the NaN weights instead: such cells silently got a pseudotime of about 0 and NaN fate probabilities, like those in #141.

## Fix

Normalise with `scipy.special.softmax`, which subtracts each cell's largest log-weight before `exp`. The weights are mathematically the same. On 50,000 synthetic cells with 500 waypoints they match master to 6e-16 wherever master's largest weight for a cell is a normal float. Between ~37.6 and 38.6 bandwidths it is subnormal and master's weights were already off, by up to 1e-4. Peak memory is unchanged.

`test_compute_pseudotime_cell_far_from_waypoints` places one cell far from all waypoints: it gets a finite pseudotime (the latest), and every cell's weights sum to 1. It fails on master. The existing `test_compute_pseudotime_equivalence` covers the output elsewhere.

#186 computes the same weights in chunks of cells, so the same one-line change applies there; I'll rebase whichever of the two merges second.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f819d5156c8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.