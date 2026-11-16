# Issue

**Title:** Drop deprecated copy keyword from astype call in from_fcs

## Description

# PR: Guard deprecated astype copy keyword by pandas version in from_fcs

## Changes

Guard the deprecated `copy` keyword of `DataFrame.astype` by pandas
version in `from_fcs`, so behaviour is preserved on every supported
version:

- `src/palantir/io.py`: module-level `PANDAS_VERSION = Version(pd.__version__)`
  (from `packaging`, already a transitive dependency of pandas), and

  ```python
  if PANDAS_VERSION < Version("3.0"):
      data = data.astype(np.float64, copy=False)
  else:
      data = data.astype(np.float64)
  ```

  — the same pattern as NVIDIA/cuml#8142.
- `README.md`: changelog entry under **Version 1.4.5**, alongside the
  pandas 3 fixes from #180.

## Verification

The `copy` keyword never affects the **result** of `astype` on any
pandas version, only whether an extra copy is made; the branch keeps
that behaviour exactly as it was on each side of the boundary. Runtime
checks on pandas 2.3.3 and 3.0.5, simulating the `from_fcs` data flow
(`fcsparser.parse`-like DataFrame → `astype` → metadata-channel filter →
`np.arcsinh(np.divide(...))`):

- pandas 2.3.3 takes the `copy=False` branch: already-`float64` columns
  still share the buffer (`np.shares_memory` = True), exactly as before
  the change; `int64` → `float64` columns allocate a new array either
  way (a dtype change cannot be done in place).
- pandas 3.0.5 takes the plain branch: no `Pandas4Warning` is emitted,
  final `arcsinh` results bit-identical to pandas 2.3.3.
- Modified files pass `python -m py_compile`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db77fbb0daac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.