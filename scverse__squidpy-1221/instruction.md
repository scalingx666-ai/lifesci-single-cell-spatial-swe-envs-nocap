# Issue

**Title:** Require Python >=3.12, test up to 3.14

## Description

Bumps the minimum supported Python to **3.12** (drops 3.11) and moves the primary test target to **3.14**.

## Changes
- `pyproject.toml`: `requires-python` and pixi python `>=3.12`; drop the 3.11 classifier; replace `py311`/`py313` pixi envs with `py312`/`py314`.
- `hatch.toml`: stable matrix now `3.12, 3.13, 3.14`.
- CI: coverage job + notebook runner move `3.13 -> 3.14`; drop the now-stale 3.11 macOS exclude.
- Docs: contributing guide.

## PEP 695 (ruff target follow-on)
The bump raises ruff's inferred target to 3.12, activating UP040/UP046/UP047.
- **UP040 adopted**: the 22 `X: TypeAlias = ...` aliases become `type X = ...`. All are annotation-only (no `get_args`/`isinstance`/`cast`/runtime reads), so the lazy `TypeAliasType` is behaviour-preserving - verified the package imports and every alias resolves.
- **UP046/UP047 ignored**: `GraphMatrixT`/`CoordT` are a shared TypeVar pair - defined in `gr.neighbors`, used by a module-level `Callable` alias, imported by `gr._build`, and re-exported from the public `squidpy.gr` API. ruff cannot autofix the cross-module use (`SpatialNeighborsResult`, which imports the TypeVar) and its fix for the local use (`GraphBuilder`) leaves the still-required exported TypeVars in place, creating dual same-name definitions. A correct conversion has to decide whether to keep exporting `GraphMatrixT` - a public-API call, out of scope for a version bump.

## Notes
- 3.13 stays a supported, tested runtime (kept in matrix + classifiers); only the dedicated coverage/default target moved to 3.14.
- Breaking for anyone still on 3.11.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e36a6f833c7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.