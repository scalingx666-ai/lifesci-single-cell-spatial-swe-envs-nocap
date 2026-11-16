# Issue

**Title:** [c++] Move column construction from ArrowAdapter to Column subclasses

## Description

**Issue and/or context:** Towards SOMA-619

**Changes:**
This moves `SOMADimension` and `SOMAGeometyColumn` construction out of the ArrowAdapter class and into the respective column classes. This is in preparation for creating C++ constructors for SOMA arrays (e.g. `SOMADataFrame`, `SOMASparseNDArray`) without first creating intermediary arrow tables.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `329cd1ea79b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.