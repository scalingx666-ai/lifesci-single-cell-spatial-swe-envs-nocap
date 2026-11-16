# Issue

**Title:** fix: use Mat.createVecs, petsc4py 3.26 removed getVecs

## Description

## Summary
`_create_solver` calls `Mat.createVecs` instead of `Mat.getVecs`, which petsc4py 3.26 removed. `createVecs` returns the same `(right, left)` pair and exists in every petsc4py release back to at least 3.12.

## Why
Fate probabilities and absorption times with `use_petsc=True` raise `AttributeError` on petsc4py 3.26; this is why the `PETSc / SLEPc + R` job has failed on `main` since 2026-10-01.

## Testing
- `TestLinearSolverPETSc`, `test_pipeline.py`, `test_gpcca.py`, `test_cflare.py` with petsc4py/slepc4py 3.26 and the pyGPCCA fix below: 227 passed, 1 xfailed.
- The job's other failures (missing coarse-grained stationary distribution, `coarse_T` plotting tests) are the same removal in pyGPCCA, fixed in GPCCA/pyGPCCA#67. The job stays red until a pyGPCCA release ships it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4bce4d90e7d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.