# Issue

**Title:** [c++] Implement experimental Memory Pool for `ManagedQuery` read operation

## Description

**Issue and/or context:** 

**Changes:**
This PR introduces a new experimental memory allocation mechanism for read operations. Instead of a per column memory budget, the new mechanism uses a global memory budget which is then split to each column based on the column byte size. 

The new mechanism allows for more predictable memory usage which is independent of the underlying array schemas.

Additionally it changes how arrow arrays are constructed regardless of the memory allocation method. Each arrow table allocates its own buffers and copies data from the `ManagedQuery` read buffers which are reused for all incomplete reads. Additionally dictionary arrays are now allocated similarly to ordinary arrays and can be reused across different columns if the use the same `Enumeration`

**Notes for Reviewer:**
The new mechanism also changes the way memory is allocated (using `resize` instead of `reserve` to avoid UB) and requires lower limits. To enable enable the new mechanism you need to set `soma.read.use_memory_pool` to `true` and `soma.read.memory_budget` (defaults to 256MB)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac5e0c597f14`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.