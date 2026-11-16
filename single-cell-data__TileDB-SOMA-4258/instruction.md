# Issue

**Title:** Adding shape validation for add_matrix_to_collection

## Description

**Issue and/or context:**
The SOMA specification defines strict requirements for the shape of layers within pre-defined collections:
```
X: (O, V)
obsm: (O, M)
varm: (V, M)
obsp: (O, O)
varp: (V, V)
```
Where` O` is the domain of `obs.soma_joinid`, `V` is the domain of `var.soma_joinid` in the containing `SOMAMeasurement`, and `M` is user-defined.

However, the `soma.io.add_matrix_to_collection()` and `soma.io.add_X_layer()` functions do not validate the shape of incoming matrices.
**Changes:**

- Introducing an internal validation function for testing the shape of the incoming Layer/Matrix to be added in a SOMA measurement.
- Tests for `add_matrix_to_collection` and `add_X_layer`

**Notes for Reviewer:**

**DEFAULT BEHAVIOR: schema_validation = **True** **

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e21bff2a5c6a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.