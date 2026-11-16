# Issue

**Title:** [r] add row/col max stat functions

## Description

# Description
Added row max and col max standalone rudimentary functions for iterable matrices.  Can handle transposed matrices.

# Tests
Tested against passing the non-iterable matrix version through MatrixStats and asserting equality
- matrices with no zeroes
- matrices with some, or all zeroes
- transposed matrices

# Thoughts
Would it make more sense to make this a method within IterableMatrix rather than a standalone function?  I see some functions in Matrix.R that aren't methods for their specific matrix class, but instead assert typing.  Not sure if that is the correct route for me to take though.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3487e3033b8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.