# Issue

**Title:** Adding `.type` property for Sparse/DenseNDArrays

## Description

**Issue and/or context:**

SOMA SparseNDArray and DenseNDArray arrays are created with a specific data type (e.g., type=pa.float32), but there is no direct way to retrieve this type via the API. Users must currently inspect the underlying Arrow schema and infer the type from there.

**Changes:**
Adding a new `property` inside the NDArray class to be inherited by both Sparse and DenseNDArray classes.

**Notes for Reviewer:**
None

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0526de09caa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.