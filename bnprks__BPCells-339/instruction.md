# Issue

**Title:** [r][cpp] add Bernoulli Sampling

## Description

Hi @bnprks,

Been sitting on this for a while, but thought I would finally PR a useful feature I've been using downstream locally with IterableMatrices (particularly for doublet simulation).

### Description

This PR adds a [Bernoulli sampling](https://en.wikipedia.org/wiki/Bernoulli_sampling) function for an `IterableMatrix` to keep each non-zero entry independently based on provided probability `prob`. So for `prob=0.3`, we expect to keep approximately 30% of non-zeros. This should require no materialization or additional allocation.

- Adds a `BernoulliSample` class that performs the streaming keep/drop filter based off of the `FilterZeros` transform.

### Details

- The sampling is designed to be deterministic. Keep/drop choice is a `splitmix64` hash of seed, column, and row.
- As the column index is taken after subset, by design, selecting the same input column multiple times will still give independent sampling not identical copies. (e.g. for doublet simulation, when `MatrixSubset` selects the same column more than once).
- Works for `uint32_t`, `float`, and `double` matrices

### Tests

- Add functional tests in `test-matrix_transforms.R`: `prob=1` no-op, keep percentage within tolerance, reproducibility, independent draws on duplicate subset columns, matrix-type invariance behaviour.

Happy to clarify any questions you might have, thanks!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adc4a3c30f60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.