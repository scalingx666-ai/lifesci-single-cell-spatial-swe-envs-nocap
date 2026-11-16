# Issue

**Title:** [r][cpp] add element-wise matrix addition

## Description

Hi @bnprks, here are the matrix addition changes we discussed.
Resolves outstanding to-do in NEWS.md and Issue #296.

### Description
Prior to this change, combining two matrices required intermediate materialization in memory with `dgCMatrix`, resulting in high memory overhead for very large matrices. This pull request adds a lazy element-wise addition of two `IterableMatrix` objects through the existing `+` operator.
- Adds a `MatrixAddition` class that iterates column-by-column and sums via a dense accumulator mirroring `SparseMultiply`.
- Overrides `colSums`/`rowSums`/`vecMultiplyRight`/`vecMultiplyLeft` via distributive/linearity properties to bypass accumulation
- Follows `MatrixMultiply` subsetting and `rbind2`/`cbind2` `merge_dimnames()` conventions.

### Behavior
- Matrix size requirements for element-wise addition are enforced (identical dimensions)
- Type coercion: mismatched matrix types promote to `double`, equal types preserved.
- Transpose: both matrices must share internal transpose states (users are pointed to `transpose_storage_order()`)

### Tests
- Added one `MatrixMath.Add` test to align with existing arithmetic-loader conventions
- Added basic addition, type coercion, transpose, dimnames, and dim-mismatch tests

### Scope
- Element-wise subtraction is not in this PR. Users can still subtract explicitly via `mat1 + (mat2 * -1)`. To discuss if subtraction should be implemented as a separate function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28759cdd5125`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.